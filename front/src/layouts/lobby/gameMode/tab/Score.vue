<template>
  <div class="score-tab">
    <h3 class="row items-baseline justify-evenly q-my-xs">{{ t('scoreTab.title') }}</h3>
    <div class="row items-baseline justify-evenly"><q-btn class="action-btn" push :label="t('scoreTab.leaderboard')" icon="mdi-format-list-bulleted" @click="showLeaderboard = !showLeaderboard"/></div>
    <q-separator spaced="md"/>
    <q-list separator>
      <q-item v-for="player in playersByScore" :key="player.id">
        <q-item-section avatar>            
          <q-icon v-if="player.id == ownerId" class="owner" name="mdi-crown"></q-icon>
          <q-icon v-else-if="!player.isConnected" color="red" name="mdi-wifi-off"></q-icon>
        </q-item-section>
        <q-item-section :class="{ self: player.id == selfId }">{{ player.pseudo }}</q-item-section>
        <q-item-section>{{ player.score }}</q-item-section>
      </q-item>
    </q-list>
  </div>
</template>
<style lang="scss">
.score-tab {
  .self, .owner {
    color: var(--clr-contrast)!important;
  }
  .self {
    font-weight: bolder;
  }
}
</style>
<script lang="ts">
import { defineComponent } from 'vue';
import { showLeaderboard } from 'store/gameLayoutManager/state';
import { playerSetup } from 'store/player';
import { useI18n } from 'vue-i18n';

export default defineComponent({
  name: 'ScoreTab',
  setup() {
    const { t } = useI18n({ useScope: 'global' });
    const {
      playersByScore,
      ownerId,
      selfId
    } = playerSetup();

    return {
      showLeaderboard,
      playersByScore,
      ownerId,
      selfId,
      t
    }
  }
});
</script>
