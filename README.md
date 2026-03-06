# Overview
This file will cover the data that the "Core" needed in order to create a new project

I think the bridge will contains 2 sets of informations requires to init the game
+ Configs
    * Slot configs
        > this configs used to determines how the slot machine board will looks like.
        > this configs also cover the animation config to spin the board, including spin duration, delays, etc.

        ```ts
        {
            {
                backgroundColor: 0x1a1a2e,
                width: 720,
                height: 450,
                slotLayout: [
                    [1, 1, 1, 1, 1],
                    [1, 1, 1, 1, 1],
                    [1, 1, 1, 1, 1],
                ],
                symbolSize: [140, 180],
                symbolGap: [-10, -35],
                reelsPosY: [-20, -20, -20, -20, -20], // Y position adjustments for each reel
                dummySymbolsAbove: 4, // Add 4 dummy symbols above visible area
                dummySymbolsBelow: 4, // Add 4 dummy symbols below visible area
                enableMasking: true, // Enable masking to hide symbols outside background
                showDummySymbols: false, // Show dummy symbols (set to false to hide all dummy symbols)
                showReelBackgrounds: false, // Show reel backgrounds/blue borders (set to false to hide)
                leftReelOnTop: true, // true = left reel on top (default), false = right reel on top
                winAnimationDelay: 0.3, // Delay before starting win animations (negative = start before last reel stops, in seconds)
                enablePrepareCascade: false, // Enable cascade effect for prepare animations (false = play all simultaneously)
                prepareCascadeDelay: 0.15, // Delay between columns in prepare cascade (in seconds)
                prepareToMatchDelay: 0.3, // Delay after prepare animations before starting match animations (in seconds)
                wildSpawnDelay: 0.5, // Delay before spawning wild from gold symbols after match (0 = immediate cascade)
                // Bonus/Free Spin configuration
                bonusConfig: {
                    delayBeforeBonusTransition: 1.0, // Delay before entering bonus mode (in seconds)
                    delayAfterBonusTransition: 0.5, // Delay after entering bonus mode before first spin (in seconds)
                    scatterMatchAnimationDelay: 0.5, // Delay after scatter match animation (in seconds)
                    delayBetweenFreeSpins: 0.3, // Delay between free spins (in seconds)
                    delayBeforeExitBonus: 1.0, // Delay before exiting bonus mode (in seconds)
                },
                // Delay before allowing next spin (after all animations complete)
                delayBeforeIdle: 0.5, // Delay in seconds before transitioning to IDLE state
                cascadeStaggerDelay: 0, // Stagger delay between simultaneous symbol drops in cascade (in milliseconds)
                cascadeEase: "bounce.out(5.5)", // Ease function for cascade animations (natural fall without too much bounce)
                cascadeMode: 'staggered', // Cascade mode: 'simultaneous' (all at once), 'sequential' (wait for completion), 'staggered' (overlapping with delays)
                cascadeInverse: true, // Cascade direction: false = left-to-right (0,1,2,3,4), true = right-to-left (4,3,2,1,0)
                cascadeReelDelay: 0.1, // Delay between each reel start (sequential mode waits for completion, staggered mode allows overlap)
                invertedData: false,
                spinConfig: {
                    spinDuration: 0.5, // Duration for each spin cycle (in seconds)
                    reelStartDelay: 0.15, // Delay between each reel starting to spin (in seconds)
                    anticipationDistance: -75, // Pull back distance before spin (negative = up)
                    anticipationDuration: 0.15, // Anticipation duration (in seconds)

                    anticipationEase: "sine.in", // Ease function for anticipation (smooth pull up)
                    spinEase: "none", // Ease function for spin (linear)
                    stopEase: "bounce.out(5.5)", // Ease function for stop/reset (bounce) "back.out(1.7)"
                    stopDuration: 0.4, // Stop reset duration (in seconds)
                    stopDelay: 0.5, // Delay before stopping after receiving API response (in seconds)
                    reelStopDuration: 0.5, // Duration for each reel to stop

                    // API integration settings
                    minimumSpinDuration: 1.0, // Minimum spin duration in seconds (keep spinning at least this long)
                    reelStopDelay: 0.10, // Delay between each reel stopping (cascade effect)
                    bounceOffset: 20, // Bounce distance in pixels (how far above target to start bounce)
                    enableBounce: true // Enable/disable bounce effect on stop
                },
                symbolDimensions: {
                    // High symbols
                    1: { width: 140, height: 180 }, // H-1
                    2: { width: 140, height: 180 }, // H-2
                    3: { width: 140, height: 180 }, // H-3
                    4: { width: 140, height: 180 }, // H-4

                    // Low symbols 
                    11: { width: 140, height: 180 }, // L-1
                    12: { width: 140, height: 180 }, // L-2
                    13: { width: 140, height: 180 }, // L-3
                    14: { width: 140, height: 180 }, // L-4
                    15: { width: 140, height: 180 }, // L-5

                    // Special symbols (always on top with higher zIndex)
                    31: { width: 200, height: 225, zIndex: 10000 }, // Scatter - always on front
                    50: { width: 175, height: 225, zIndex: 10000 }, // Wild - always on front
                }
            };
        }
        ```

    * Symbol configs
        > this configs contain information of the symbol, including types, texture, paytable.

    * Localization configs
        > this configs contains information of the URL of the spreadsheet where localization data is saved

        ```ts
        public static readonly GOOGLE_SHEET_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTml1MDfwRAVMHGT9R884MId6oBHYEOvABUfdz8gn9xQ2o8ozEbx9u13v99-L84E33V8dLt9-A9ps5L/pub?output=csv';
        ```

    * Buy Feature configs
        > this configs contain information of feature list, id, multiplier (cost), texture
    
        ```ts
        static readonly FEATURES: BuyFeatureItemConfig[] = [
            {
                featureId: 1,
                multiplier: 1000,
                background: "bfFeatureBg"
            },
            {
                featureId: 2,
                multiplier: 1,
                background: "bfFeatureBg"
            },
            {
                featureId: 2,
                multiplier: 1,
                background: "bfFeatureBg"
            },
            {
                featureId: 2,
                multiplier: 1,
                background: "bfFeatureBg"
            },
            {
                featureId: 2,
                multiplier: 1,
                background: "bfFeatureBg"
            },
        ];
        ```

    + Loading configs
        > this configs contain informations of the loading screen, including textures, hint.

        ```ts
        export const LoadingConfig = {
            // Timing
            HINT_ROTATION_INTERVAL: 3000,  // 3 seconds per hint
            MIN_LOADING_DURATION: 2000,    // Minimum display time
            PROGRESS_BAR_TWEEN_DURATION: 0.3,

            // Loading tips array
            TIPS: [
                { text: "Collect 3 or more Scatter symbols to trigger Free Spins!" },
                { text: "Wild symbols substitute for all regular symbols." },
                { text: "Golden symbols transform into Wilds during wins!" },
                { text: "Higher bets unlock bigger multiplier potential." },
                { text: "Use Turbo mode for faster spins." },
            ] as LoadingTip[],

            // Progress bar dimensions (based on asset dimensions)
            PROGRESS_BAR: {
                width: 600,
                height: 30,
                glowOffset: 10,  // Glow extends beyond bar
            },
        };
        ```

    + Default configs
        > this configs contain information of default board.

        ```ts
        static readonly INIT_BOARD = [
        [31, 14, 11, 1],
        [15, 31, 3, 15, 4],
        [31, 14, 1, 14, 11],
        [12, 12, 15, 3, 11],
        [4, 12, 3, 4]
        ];
        ```

    * Buy Feature popup configs
        > this configs contain information of the buy feature popups, including position of title, button position, etc.

    * Bet Options popup configs
        > this configs contain informations of the bet options popup, including position of title, button position, etc.

    * Spin options popup configs
        > this configs contain informations of the spin options popup, including position of title, button position, etc.

    * Game info popup configs
        > this configs contain informations of the game info popup, including position of title, button position, etc.

    * History popup configs
        > this configs contain informations of the history popup, including position of title, button position, etc.

    * Big win popup configs
        > this configs contain informations of big win popup, including animation duration, upgrade animation every n * bet, etc.

    * Total freespins popup configs
        > this configs contain informations of total freespins popup, including animation duration, etc.

    * Total win popup configs
        > this configs contain informations of total win popup, including animation duration, etc.

+ Components
    * LoadScreen
        
        ```ts
        {
            background: 'file-name.format',
            bar: ''
            bar-bg: '',
            bar-mask: ''
        }
        ```
    
    * Buttons
        
        ```ts
        {
            bet-opt-btn: 'file-name.format',
            history-btn:
            info-btn: 
            menu-btn:
            menu-close-btn:
            sound-btn-off:
            sound-btn-on:
            spin-opt-btn:
            buy-feature-btn:
        }
        ```
    
    * Bet Options Popup

        ```ts
        {
            title
            bg
            closeBtn
            confirmButton
        }
        ```

    * Balance UI

        ```ts
        {
            
        }
        ```

    * Quick Option

        ```ts
        {
            
        }
        ```

    * Bet Slider

        ```ts
        {
            
        }
        ```
    
    * Spin Options Popup

        ```ts
        {
            
        }
        ```

    * History Popup
        > History popup covers 4 components: 


    * Big Win Popup
        > Big win popup will need information of big win skeleton.

        ```ts
        {
            bigwin-skel:
            bigwin-atlas:
            bigwin-png:
            animations: [] // I think this one should be fixed / standardized..
        }
        
        ```
    
    * Total Win Popup

        ```ts
        {
            skel:
            atlas:
            png:
            animations: [] 
        }
        
        ```

    * Total Free Spins Popup

        ```ts
            {
                skel:
                atlas:
                png:
                animations: [] 
            }
            
        ```

    * Win UI

        ```ts
        {
            
        }
        ```

    * Reward Information

        ```ts
        {
            skel: 
            atlas:
            png:
            hint: []
        }
        ```
    * Background Manager

        ```ts
        {
            
        }
        ```

    * Sound / Feature?



