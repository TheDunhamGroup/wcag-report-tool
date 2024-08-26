<!-- @Layout:Base -->
<div id="site-header">
  <a href="https://dunhamweb.com/"><img
    alt="Dunham Web"
    src={`${$basepath}/images/dunham.svg`}
  /></a>
  <span style="font-size: xx-large;">WCAG-EM Report Tool</span>
  <span>
    <a href="http://w3.org/"><img
      alt="W3C"
      src={`${$basepath}/images/w3c.svg`}
    /></a>
  <a href="https://w3.org/WAI/"><img
      alt="Web Accessibility Initiative"
      src={`${$basepath}/images/wai.svg`}
    /></a>
  </span>
</div>

<NavigationBar />

<slot />

{#if !isAcknowledgements}
<Pager label="{TRANSLATED.STEP}" context="{pagerContext}" />
{/if}

<!-- /@Layout -->

<style>
  .BaseLayout {
    padding: 2em 1em;
  }

  .Controls {
    font-size: 0.8125em;
  }

  @media (min-width: 60em) {
    .BaseLayout {
      padding: 2em 0;
    }
  }

  #site-header {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 1em;
  }

  #site-header img{
    height: 4em;
  }
</style>

<script>
  import { getContext } from 'svelte';
  import { useLocation } from 'svelte-navigator';

  import { routes, basepath } from '@app/stores/appStore.js';
  import locales from '@app/locales/index.json';

  import LanguageSelect from '@app/components/ui/LanguageSelect.svelte';
  import NavigationBar from '@app/components/ui/NavigationBar.svelte';
  import Pager from '@app/components/ui/Pager.svelte';

  const { translate } = getContext('app');
  const location = useLocation();

  $: TRANSLATED = {
    STEP: $translate('UI.NAV.STEP', { default: 'step' }),
  };

  $: isAcknowledgements = $location.pathname === $routes.ACKNOWLEDGEMENTS.path;

  $: pagerContext = Object.keys($routes).map((key) => {
    return $routes[key];
  });  
</script>
