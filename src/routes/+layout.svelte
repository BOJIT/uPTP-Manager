<!--
 * @file +layout.svelte
 * @author James Bennion-Pedley
 * @brief Example top-level layout
 * @date 27/12/2024
 *
 * @copyright Copyright (c) 2024
 *
-->

<script lang="ts">
    /*-------------------------------- Imports -------------------------------*/

    import { App, UI } from '@bojit/svelte-components';
    import { type Icon } from '@bojit/svelte-components/icons';

    import PaintBrush from 'carbon-icons-svelte/lib/PaintBrush.svelte';
    import LogoGithub from 'carbon-icons-svelte/lib/LogoGithub.svelte';

    import logo from '$lib/assets/logo.png';

    import '../app.css';

    /*--------------------------------- Props --------------------------------*/

    let { children } = $props();

    let app: App;

    /*-------------------------------- Methods -------------------------------*/

    /*------------------------------- Lifecycle ------------------------------*/
</script>

<svelte:head><title>µPTP Manager</title></svelte:head>

<App defaultMode="system" bind:this={app}>
    <UI.NavBar
        title="µPTP Manager"
        {logo}
        logoLink="https://github.com/BOJIT/uPTP"
        themeOverride="dark"
        items={[
            {
                type: 'button',
                icon: LogoGithub as Icon,
                label: 'Source Code',
                link: 'https://github.com/BOJIT/uPTP',
                visibility: 'desktop'
            },
            {
                type: 'separator',
                visibility: 'desktop'
            },
            {
                type: 'button',
                icon: PaintBrush as Icon,
                label: 'Set Theme',
                visibility: 'desktop',
                onclick: () => {
                    app.launchThemeSelector();
                }
            }
        ]}
    />
    {@render children()}
</App>
