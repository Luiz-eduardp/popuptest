<template>
  <q-layout view="lHr lpR lFr">
    <q-header reveal elevated class="bg-primary text-black" height-hint="98">
      <q-toolbar align="center">
        <q-toolbar-title>
          <q-avatar>
            <img src="../assets/icon.png" />
          </q-avatar>
          Jackpot PRO
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="center">
        <q-route-tab to="/regras" label="Regulamentos" />
        <q-route-tab to="/sacar" label="Sacar" />
        <q-route-tab to="/comprarvip" label="Comprar Vip" />
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view class="q-pa-md q-gutter-sm" />
    </q-page-container>
  </q-layout>
</template>
