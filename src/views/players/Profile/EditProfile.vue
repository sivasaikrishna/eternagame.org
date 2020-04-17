<template>
  <EternaPage v-if="player" title="Player Profile">
    <EditField />

    <template #sidebar="{ isInSidebar }">
      <DropdownSidebarPanel
        :options="options"
        paramName="sort"
        replace
        :isInSidebar="isInSidebar"
      />
    </template>
  </EternaPage>
</template>

<script lang="ts">
  import { Component, Vue, Mixins } from 'vue-property-decorator';
  import { RouteCallback, Route } from 'vue-router';
  import { AxiosInstance } from 'axios';
  import EternaPage from '@/components/PageLayout/EternaPage.vue';
  import DropdownSidebarPanel, { Option } from '@/components/Sidebar/DropdownSidebarPanel.vue';
  import PageDataMixin from '@/mixins/PageData';
  import EditField from './components/EditField.vue';
  //   import LabViewData, { LabData } from './types';

  async function fetchPageData(route: Route, http: AxiosInstance) {
    return (await http.get(`/get/?type=user&uid=${route.params.uid}`)).data.data;
  }

  Component.registerHooks(['beforeDestroy']);

  @Component({
    components: {
      EternaPage,
      DropdownSidebarPanel,
      EditField,
    },
  })
  export default class EditProfile extends Mixins(PageDataMixin(fetchPageData)) {
    get player() {
      return {};
    }

    private options: Option[] = [
      { value: 'about', text: 'About' },
      { value: 'achievements', text: 'Achievements' },
      { value: 'synthesized', text: 'Synthesized RNAs' },
      { value: 'latest', text: 'Latest Activity' },
      { value: 'created', text: 'Created Puzzles' },
    ];

    private picture: string = `${process.env.VUE_APP_API_BASE_URL}/sites/default/files/pictures/picture-133043.png`;

    // private picture: string = 'https://graph.facebook.com/10220887579400634/picture?type=normal';

    private playerName: string = 'Iroppy';

    private playerRank: string = '1';

    private aboutMeText: string = `Live in sometimes hot/often very cold land of 10,000 lakes (Minnesota).
      Univ of Chicago BA/MBA <br/>
      —now on 2nd career as software product manager at IBM.<br/>
      —first career was public & non-profit financial management<br/>
      Passions: racquetball, science, great software, sci-fi, Go, social justice, eteRNA.<br/>
      <br/>
      <b>ete-RNA-L eteRNA wisDOM:</b>
      • When in doubt (or bored) strengthen.<br/>
      • When in doubt on Switch Puzzles: Reset!<br/>
      • When an designer titles a puzzle “ugly”, take their word for it.<br/>
      • When an designer titles a puzzle something and “easy”, run away.<br/>
      • Credit your mods.<br/>
      • Lab results are in the mail.<br/>
      • Going on a diet to reduce a few GCs.<br/>
      • These aren’t the GUs you are looking for. Move along…<br/>
      <br/><br/>

      <b>ETERNACON 2015!</b>`;
  }
</script>

<style lang="scss" scoped>
  @import '@/styles/global.scss';

  .about-me {
    font-size: 1.375rem;
    font-weight: bold;
  }

  .about-me-text {
    max-width: 710px;
  }

  .player-name {
    font-size: 1.625rem;
    font-weight: bold;
    margin-bottom: 0px;
    width: 300px;
  }

  .player-details {
    margin-top: 20px;
    width: 100%;
  }

  .player-rank {
    font-size: 1.0625rem;
    font-weight: bold;
    margin-bottom: 0px;
    margin-top: 10px;
    margin-right: 250px;
  }

  .player-image {
    object-fit: scale-down;
    margin-right: 20px;
    width: 61.58px;
    height: 61.58px;
  }

  .player-image-large {
    width: 115.93px;
    height: 115.93px;
    object-fit: scale-down;
    margin-right: 20px;
  }
</style>
