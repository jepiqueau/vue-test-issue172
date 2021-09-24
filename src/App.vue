<template>
  <ion-app>
      <jeep-sqlite />
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import { defineComponent, onMounted } from 'vue';
import { Capacitor } from '@capacitor/core';
import { createTablesNoEncryption, importTwoUsers,
  dropTablesTablesNoEncryption } from '@/utils/utils-db-no-encryption';
import { CapacitorSQLite, SQLiteConnection } from "@capacitor-community/sqlite";

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  },
  setup() {
    console.log(`on App Setup`)
    let errMess = "";
    const platform = Capacitor.getPlatform();
    // Create an SQLite connection
    const sqliteConnection = new SQLiteConnection(CapacitorSQLite);
    const noEncryptionTest = async (): Promise<boolean>  => {
      try {
        let db;
        if (
          !(await sqliteConnection.isConnection("db-issue172")).result ||
          !(await sqliteConnection.checkConnectionsConsistency()).result
        ) {
          // Create a connection to the db_issue172 db
          db = await sqliteConnection.createConnection("db-issue172", false, "no-encryption", 1);
          // Open the MY_DB db
          await db.open();
        } else {
          // Get existing db connection
          console.log("in retrieveConnection");
          db = await sqliteConnection.retrieveConnection("db-issue172");
        }
        // Drop tables if exists
        let res = await db.execute(dropTablesTablesNoEncryption);
        if(typeof res.changes === "object" && typeof res.changes.changes === "number" && res.changes.changes !== 0 &&
                    res.changes.changes !== 1){
            errMess = `Execute dropTablesTablesNoEncryption changes < 0`;
            return false;
        } 
        // Create tables
        res = await db.execute(createTablesNoEncryption);
        if (typeof res.changes === "object" && typeof res.changes.changes === "number" && res.changes.changes < 0) {
            errMess = `Execute createTablesNoEncryption changes < 0`;
            return false;
        }


        // Insert two users with execute method
        res = await db.execute(importTwoUsers);
        if (typeof res.changes === "object" && typeof res.changes.changes === "number" && res.changes.changes !== 2) {
            errMess = `Execute importTwoUsers changes != 2`;
            return false;
        }
        if(platform === "web") {
          // save the database
          await sqliteConnection.saveToStore("db-issue172");
        }
        // Select all Users
        let resVal = await db.query("SELECT * FROM users");
        if(typeof resVal.values === "object" && (resVal.values.length !== 2 ||
                    resVal.values[0].name !== "Whiteley" ||
                    resVal.values[1].name !== "Jones")) {
            errMess = `Query not returning 2 values`;
            return false;
        }
        // Close Connection NoEncryption        
        await sqliteConnection.closeConnection("db-issue172"); 
        return true;
      } catch (err) {
        errMess = `${err}`;
        return false;
      }
    };

    onMounted(async () => {
      console.log(`on App onMounted`)
      let retNoEncryption: boolean
      if(platform === "web") {
        await customElements.whenDefined('jeep-sqlite');
        const jeepSqliteEl = document.querySelector('jeep-sqlite');
        if(jeepSqliteEl != null) {
          await sqliteConnection.initWebStore()
          retNoEncryption = await noEncryptionTest();
        } else {
          console.log('$$ jeepSqliteEl is null');
          retNoEncryption = false;
        }
      } else {
          retNoEncryption = await noEncryptionTest();
      }
      if(!retNoEncryption) {
        console.log(`error message: ${errMess}`)
          console.log("The testDatabaseNoEncryption failed");
      } else {
          console.log("The testDatabaseNoEncryption was successful");
      }
    });
    return {platform, sqliteConnection, errMess}
  }
});
</script>