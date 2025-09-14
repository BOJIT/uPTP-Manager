<!--
 * @file +page.svelte
 * @author James Bennion-Pedley
 * @brief Main application layout
 * @date 14/09/2025
 *
 * @copyright Copyright (c) 2025
 *
-->

<script lang="ts">
    /*-------------------------------- Imports -------------------------------*/

    import { UI } from '@bojit/svelte-components';

    import { invoke } from '@tauri-apps/api/core';

    import { PaneGroup, Pane as PaneItem, PaneResizer } from 'paneforge';

    /*--------------------------------- Props --------------------------------*/

    /*-------------------------------- Methods -------------------------------*/

    /*------------------------------- Lifecycle ------------------------------*/

    let name = $state('');
    let greetMsg = $state('');

    async function greet(event: Event) {
        event.preventDefault();
        // Learn more about Tauri commands at https://tauri.app/develop/calling-rust/
        greetMsg = await invoke('greet', { name });
    }
</script>

<main>
    <PaneGroup direction="horizontal" class="p-1">
        <PaneItem defaultSize={60} class="rounded-sm bg-accent">
            <UI.Tabs tabs={['Management', 'GPS', 'Clock']}></UI.Tabs>
        </PaneItem>
        <PaneResizer
            class="relative flex w-1 items-center justify-center bg-background hover:bg-blue-400 active:bg-blue-400"
        />
        <PaneItem defaultSize={40} class="rounded-sm bg-accent">
            <UI.Content>
                <h4>Devices</h4>
                <hr />
            </UI.Content>
        </PaneItem>
    </PaneGroup>
</main>

<style>
    main {
        flex: 2 0 auto;
        position: relative;
    }

    main > :global(div) {
        position: absolute;
        top: 0px;
        bottom: 0px;
        left: 0px;
        right: 0px;
    }

    main :global(h6) {
        font-weight: 200;
        font-size: 0.85em;
    }

    h4 {
        margin: 0px !important;
        text-align: center;
    }

    hr {
        margin-top: 0.4rem !important;
    }
</style>
