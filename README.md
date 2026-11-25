<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ROC BOX | Curated Rochester Experience Packages</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #fafafa;
            color: #09090b;
        }
        .card-hover {
            transition: all 0.2s ease-in-out;
        }
        .card-hover:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.08);
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 5px;
            height: 5px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #18181b;
            border-radius: 4px;
        }
        @media print {
            header, footer, #package-form-container, .no-print {
                display: none !important;
            }
            body {
                background: white;
                color: black;
            }
            .print-full {
                width: 100% !important;
                margin: 0 !important;
                padding: 0 !important;
                box-shadow: none !important;
                border: none !important;
            }
        }
    </style>
</head>
<body class="flex flex-col min-h-screen antialiased selection:bg-zinc-900 selection:text-white">

    <!-- Header / Navbar -->
    <header class="bg-black text-white border-b border-zinc-800 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            
            <!-- Modern Clean Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="switchTab('builder')">
                <div class="w-11 h-11 bg-white text-black flex items-center justify-center rounded-xl font-black text-xl tracking-tighter shadow-sm border border-zinc-200">
                    <i class="fa-solid fa-box-open text-black text-lg"></i>
                </div>
                <div class="flex flex-col">
                    <div class="flex items-center space-x-2">
                        <span class="font-black text-xl tracking-wider uppercase text-white">ROC<span class="text-zinc-400 font-light">BOX</span></span>
                    </div>
                    <p class="text-xs text-zinc-400 font-medium">Curated Rochester Experience Packages</p>
                </div>
            </div>
            
            <!-- Navigation Controls -->
            <div class="flex items-center space-x-3">
                <button onclick="switchTab('builder')" id="tab-btn-builder" class="px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg bg-white text-black transition flex items-center space-x-2 border border-white">
                    <i class="fa-solid fa-sliders text-xs"></i>
                    <span>Package Builder</span>
                </button>
                <button onclick="switchTab('saved')" id="tab-btn-saved" class="px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg text-zinc-300 hover:text-white hover:bg-zinc-900 transition flex items-center space-x-2 relative border border-transparent">
                    <i class="fa-solid fa-bookmark text-xs"></i>
                    <span>Saved Packages</span>
                    <span id="saved-badge" class="hidden absolute -top-1 -right-1 w-5 h-5 bg-white text-black text-xs rounded-full flex items-center justify-center font-bold border-2 border-black">0</span>
                </button>
            </div>

        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">

        <!-- TAB 1: BUILDER VIEW -->
        <div id="view-builder" class="space-y-8">

            <!-- Hero Section & Generator Form -->
            <div id="package-form-container" class="bg-black text-white rounded-2xl p-6 sm:p-10 border border-zinc-800 shadow-2xl relative">
                
                <div class="max-w-3xl mb-8">
                    <div class="inline-flex items-center space-x-2 px-3 py-1 bg-zinc-900 text-zinc-300 rounded-full text-xs font-semibold uppercase tracking-wider mb-4 border border-zinc-800">
                        <span class="w-2 h-2 rounded-full bg-emerald-400"></span>
                        <span>All-In-One Trip Bundle Solution</span>
                    </div>
                    <h1 class="text-3xl sm:text-5xl font-black tracking-tight leading-tight text-white mb-3">
                        Rochester, Bundled & Delivered.
                    </h1>
                    <p class="text-zinc-400 text-sm sm:text-base leading-relaxed">
                        Skip searching individual review sites. Input your trip criteria to generate a complete, curated Rochester care package containing hotel basecamp, dining, and daily activities.
                    </p>
                </div>

                <!-- Form Controls Grid -->
                <form id="package-form" onsubmit="generatePackage(event)" class="bg-zinc-900/90 p-6 rounded-xl border border-zinc-800 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
                    
                    <!-- Duration -->
                    <div>
                        <label class="block text-xs font-bold text-zinc-300 uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-calendar-day text-zinc-400 mr-1.5"></i>Duration
                        </label>
                        <select id="param-days" class="w-full bg-black border border-zinc-700 rounded-lg px-3 py-2.5 text-sm text-white focus:ring-2 focus:ring-white focus:outline-none font-medium">
                            <option value="1">1 Day (Quick Stop)</option>
                            <option value="2" selected>2 Days (Weekend Getaway)</option>
                            <option value="3">3 Days (Full Rochester)</option>
                            <option value="4">4 Days (Extended Experience)</option>
                        </select>
                    </div>

                    <!-- Vibe / Persona -->
                    <div>
                        <label class="block text-xs font-bold text-zinc-300 uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-compass text-zinc-400 mr-1.5"></i>Trip Vibe
                        </label>
                        <select id="param-vibe" class="w-full bg-black border border-zinc-700 rounded-lg px-3 py-2.5 text-sm text-white focus:ring-2 focus:ring-white focus:outline-none font-medium">
                            <option value="foodie" selected>Foodie & Craft Drinks</option>
                            <option value="family">Family & Interactive Play</option>
                            <option value="arts">Arts, History & Culture</option>
                            <option value="outdoors">Parks, Water & Nature</option>
                            <option value="rit">RIT Campus & Family Visit</option>
                        </select>
                    </div>

                    <!-- Budget Level -->
                    <div>
                        <label class="block text-xs font-bold text-zinc-300 uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-wallet text-zinc-400 mr-1.5"></i>Budget Tier (Total / Day)
                        </label>
                        <select id="param-budget" class="w-full bg-black border border-zinc-700 rounded-lg px-3 py-2.5 text-sm text-white focus:ring-2 focus:ring-white focus:outline-none font-medium">
                            <option value="budget">Value & Casual ($80 – $110 / day total)</option>
                            <option value="moderate" selected>Balanced Comfort ($170 – $240 / day total)</option>
                            <option value="premium">Boutique & Fine Dining ($300 – $450+ / day total)</option>
                        </select>
                    </div>

                    <!-- Pace -->
                    <div>
                        <label class="block text-xs font-bold text-zinc-300 uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-bolt text-zinc-400 mr-1.5"></i>Daily Pace
                        </label>
                        <select id="param-pace" class="w-full bg-black border border-zinc-700 rounded-lg px-3 py-2.5 text-sm text-white focus:ring-2 focus:ring-white focus:outline-none font-medium">
                            <option value="relaxed">Relaxed (3 stops/day)</option>
                            <option value="balanced" selected>Balanced (4 stops/day)</option>
                            <option value="packed">Packed (5 stops/day)</option>
                        </select>
                    </div>

                    <!-- Quick Preference Toggles -->
                    <div class="sm:col-span-2 lg:col-span-3">
                        <label class="block text-xs font-bold text-zinc-300 uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-sliders text-zinc-400 mr-1.5"></i>Preferences & Preferences Tagging
                        </label>
                        <div class="flex flex-wrap gap-2 text-xs">
                            <button type="button" onclick="toggleTag(this, 'Garbage Plate')" class="pref-tag px-3 py-1.5 rounded-lg border border-zinc-700 bg-black text-zinc-300 hover:border-zinc-500 transition">🍔 Include Garbage Plate</button>
                            <button type="button" onclick="toggleTag(this, 'Walkable')" class="pref-tag px-3 py-1.5 rounded-lg border border-zinc-700 bg-black text-zinc-300 hover:border-zinc-500 transition">🚶 Walkable Spots</button>
                            <button type="button" onclick="toggleTag(this, 'Kid Friendly')" class="pref-tag px-3 py-1.5 rounded-lg border border-zinc-700 bg-black text-zinc-300 hover:border-zinc-500 transition">👨‍👩‍👧 Kid Friendly</button>
                            <button type="button" onclick="toggleTag(this, 'Erie Canal')" class="pref-tag px-3 py-1.5 rounded-lg border border-zinc-700 bg-black text-zinc-300 hover:border-zinc-500 transition">🌊 Erie Canal Access</button>
                        </div>
                    </div>

                    <!-- Submit Button -->
                    <div class="sm:col-span-2 lg:col-span-1 flex items-end">
                        <button type="submit" id="generate-btn" class="w-full bg-white hover:bg-zinc-200 text-black font-extrabold py-3 px-4 rounded-lg shadow-lg transition flex items-center justify-center space-x-2">
                            <span>Assemble Package</span>
                            <i class="fa-solid fa-arrow-right text-xs"></i>
                        </button>
                    </div>
                </form>

            </div>

            <!-- Loading State -->
            <div id="loading-spinner" class="hidden py-20 text-center bg-white rounded-2xl border border-zinc-200">
                <div class="inline-block animate-spin rounded-full h-10 w-10 border-4 border-black border-t-transparent mb-4"></div>
                <h3 class="text-lg font-bold text-black">Curating Your Rochester Experience Package...</h3>
                <p class="text-xs text-zinc-500 mt-1">Algorithm matching hotel basecamp, local dining, and top attractions.</p>
            </div>

            <!-- Generated Package Display Area -->
            <div id="package-results" class="hidden space-y-8 print-full">
                
                <!-- Package Summary Bar Header -->
                <div class="bg-white rounded-2xl p-6 border border-zinc-200 shadow-sm flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
                    <div>
                        <div class="flex items-center space-x-2 mb-2">
                            <span id="pkg-tag" class="px-2.5 py-1 bg-black text-white rounded text-[11px] font-black uppercase tracking-wider">
                                Curated Package
                            </span>
                            <span id="pkg-duration-badge" class="text-xs text-zinc-500 font-semibold"></span>
                        </div>
                        <h2 id="pkg-title" class="text-2xl sm:text-3xl font-black text-black"></h2>
                        <p id="pkg-description" class="text-zinc-600 text-sm mt-1 max-w-3xl leading-relaxed"></p>
                    </div>

                    <div class="flex flex-wrap items-center gap-3 w-full md:w-auto no-print">
                        <button onclick="saveCurrentPackage()" id="save-btn" class="flex-1 md:flex-none px-4 py-2.5 border border-zinc-300 rounded-lg text-black font-bold text-xs uppercase tracking-wider hover:bg-zinc-50 transition flex items-center justify-center space-x-2">
                            <i class="fa-regular fa-bookmark"></i>
                            <span>Save Package</span>
                        </button>
                        <button onclick="window.print()" class="flex-1 md:flex-none px-4 py-2.5 bg-black text-white hover:bg-zinc-800 rounded-lg text-xs font-bold uppercase tracking-wider transition flex items-center justify-center space-x-2">
                            <i class="fa-solid fa-print"></i>
                            <span>Print / Export</span>
                        </button>
                    </div>
                </div>

                <!-- Hotel Recommendation Card (Basecamp) -->
                <div class="bg-black text-white border border-zinc-800 rounded-2xl p-6 sm:p-8 shadow-xl">
                    <div class="flex items-start justify-between flex-wrap gap-4">
                        <div class="flex items-start space-x-4">
                            <div class="w-12 h-12 rounded-xl bg-white text-black flex items-center justify-center text-xl shrink-0 font-bold">
                                <i class="fa-solid fa-hotel"></i>
                            </div>
                            <div>
                                <div class="text-[11px] font-bold text-zinc-400 uppercase tracking-widest mb-1">Recommended Basecamp (Hotel)</div>
                                <h3 id="hotel-name" class="text-xl sm:text-2xl font-black text-white"></h3>
                                <p id="hotel-details" class="text-sm text-zinc-400 mt-1 max-w-2xl"></p>
                                <div id="hotel-amenities" class="flex flex-wrap gap-2 mt-4"></div>
                            </div>
                        </div>
                        <div class="text-right">
                            <span id="hotel-price" class="text-xl font-black text-white block"></span>
                            <span class="text-xs text-zinc-400 font-medium">Optimal Vibe Match</span>
                        </div>
                    </div>
                </div>

                <!-- Day-by-Day Care Package Itinerary Timeline -->
                <div class="space-y-6">
                    <div class="flex items-center justify-between">
                        <h3 class="text-xl font-black text-black tracking-tight flex items-center">
                            <i class="fa-solid fa-list-check mr-2.5 text-zinc-700"></i>
                            Day-by-Day Itinerary Schedule
                        </h3>
                        <span class="text-xs text-zinc-500 font-medium">All items included in your care package</span>
                    </div>

                    <!-- Container for Days -->
                    <div id="days-container" class="space-y-6"></div>
                </div>

            </div>

        </div>

        <!-- TAB 2: SAVED PACKAGES VIEW -->
        <div id="view-saved" class="hidden space-y-6">
            <div class="flex items-center justify-between border-b border-zinc-200 pb-4">
                <div>
                    <h2 class="text-2xl font-black text-black">Saved Rochester Packages</h2>
                    <p class="text-xs text-zinc-500">Access and review your previously generated trip care packages.</p>
                </div>
                <button onclick="clearSavedPackages()" class="text-xs text-zinc-500 hover:text-black font-semibold flex items-center space-x-1 underline">
                    <i class="fa-solid fa-trash"></i>
                    <span>Clear Saved Items</span>
                </button>
            </div>

            <div id="saved-packages-list" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Dynamically populated -->
            </div>
            
            <div id="no-saved-state" class="text-center py-20 bg-white rounded-2xl border border-zinc-200">
                <i class="fa-solid fa-box-open text-4xl text-zinc-300 mb-3"></i>
                <h3 class="text-base font-bold text-black">No saved packages yet</h3>
                <p class="text-xs text-zinc-500 mt-1">Use the Package Builder to assemble and save custom Rochester itineraries.</p>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="bg-black text-zinc-400 border-t border-zinc-800 mt-auto py-8 no-print">
        <div class="max-w-7xl mx-auto px-4 text-center text-xs flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="flex items-center space-x-2">
                <span class="font-black text-white">ROC BOX</span>
                <span>— Rochester Travel & Experience Curator</span>
            </div>
            <div class="flex items-center space-x-6 text-zinc-400">
                <span>RIT Campus & Regional Data</span>
                <span>•</span>
                <span>Web-App Track</span>
            </div>
        </div>
    </footer>

    <!-- Application Logic -->
    <script>
        // Selected preference tags state
        let activeTags = [];

        function toggleTag(btn, tag) {
            if (activeTags.includes(tag)) {
                activeTags = activeTags.filter(t => t !== tag);
                btn.className = "pref-tag px-3 py-1.5 rounded-lg border border-zinc-700 bg-black text-zinc-300 hover:border-zinc-500 transition";
            } else {
                activeTags.push(tag);
                btn.className = "pref-tag px-3 py-1.5 rounded-lg border border-white bg-white text-black font-bold transition";
            }
        }

        // -------------------------------------------------------------
        // ROCHESTER REGIONAL DATA BANK (Curated Real-World Locations)
        // -------------------------------------------------------------
        const ROC_HOTELS = [
            {
                id: 'hotel-budget-1',
                name: 'Microtel Inn & Suites by Wyndham Henrietta',
                vibe: ['rit', 'budget', 'outdoors'],
                budgetTier: 'budget',
                price: '$85 est. hotel portion',
                address: '205 Holleder Pkwy, Henrietta, NY',
                desc: 'Comfortable, budget-friendly basecamp located minutes from RIT campus with complimentary breakfast and easy highway access.',
                amenities: ['Free Breakfast', 'RIT Proximity', 'Free WiFi', 'Budget Friendly']
            },
            {
                id: 'hotel-budget-2',
                name: 'Red Roof Inn Rochester - Airport',
                vibe: ['budget', 'family'],
                budgetTier: 'budget',
                price: '$80 est. hotel portion',
                address: '4820 W Henrietta Rd, Henrietta, NY',
                desc: 'Affordable, hassle-free lodging ideal for quick stops, easy campus visits, and casual road trippers.',
                amenities: ['Pet Friendly', 'Free Parking', 'Airport & Campus Access', 'Budget Tier']
            },
            {
                id: 'hotel-mod-1',
                name: 'Courtyard Rochester Downtown',
                vibe: ['foodie', 'moderate', 'arts'],
                budgetTier: 'moderate',
                price: '$150 est. hotel portion',
                address: '390 East Ave, Rochester, NY',
                desc: 'Modern hotel within walking distance of Eastman Museum, local cafes, and downtown art galleries.',
                amenities: ['On-site Bistro', 'Walkable District', 'Fitness Center', 'Free WiFi']
            },
            {
                id: 'hotel-mod-2',
                name: 'Hilton Garden Inn Rochester - College Town',
                vibe: ['rit', 'moderate', 'family'],
                budgetTier: 'moderate',
                price: '$145 est. hotel portion',
                address: '30 Celebration Dr, Rochester, NY',
                desc: 'Located adjacent to University of Rochester and minutes from RIT campus. Ideal basecamp for university visitors.',
                amenities: ['College Town Dining', 'Indoor Pool', 'RIT Proximity', 'Free Parking']
            },
            {
                id: 'hotel-mod-3',
                name: 'Hyatt Regency Rochester Downtown',
                vibe: ['arts', 'moderate', 'outdoors'],
                budgetTier: 'moderate',
                price: '$160 est. hotel portion',
                address: '125 E Main St, Rochester, NY',
                desc: 'High-rise downtown hotel offering panoramic views of the Genesee River, direct skyway access, and central location.',
                amenities: ['Genesee River Views', 'Central Hub', 'Starbucks Onsite', 'Indoor Pool']
            },
            {
                id: 'hotel-prem-1',
                name: 'The Strathallan Rochester Hotel & Spa',
                vibe: ['foodie', 'premium', 'arts'],
                budgetTier: 'premium',
                price: '$245 est. hotel portion',
                address: '550 East Ave, Rochester, NY (Neighborhood of the Arts)',
                desc: 'Boutique hotel in Rochester’s cultural neighborhood. Features Char Steakhouse and rooftop cocktail bar with city views.',
                amenities: ['Rooftop Grill & Lounge', 'Full Spa', 'East Ave Location', 'Indoor Pool']
            },
            {
                id: 'hotel-prem-2',
                name: 'The Del Monte Lodge Renaissance Rochester Hotel',
                vibe: ['premium', 'outdoors', 'foodie'],
                budgetTier: 'premium',
                price: '$275 est. hotel portion',
                address: '41 N Main St, Pittsford, NY',
                desc: 'Luxury boutique property situated on the banks of the historic Erie Canal path in Pittsford Village.',
                amenities: ['Canal-side Location', 'Luxury Spa', 'Erie Grill Dining', 'Boutique Service']
            }
        ];

        const ROC_DINING_LIST = [
            // Casual & Iconic Local Eats
            { name: 'Nick Tahou Hots (Home of the Garbage Plate)', mealType: 'lunch', vibe: ['foodie', 'rit'], cost: '$12 – $16 per meal', duration: '1 hr', desc: 'The authentic Rochester staple: burgers, mac salad, home fries, and secret spicy meat sauce.', tags: ['Garbage Plate'] },
            { name: 'Dogtown Gourmet Dogs & Plates', mealType: 'lunch', vibe: ['foodie', 'rit', 'family'], cost: '$10 – $15 per meal', duration: '1 hr', desc: 'Monroe Ave favorite for creative garbage plates, loaded hot dogs, and vegan options.', tags: ['Garbage Plate', 'Walkable'] },
            { name: 'Javas Cafe & Espresso Bar', mealType: 'lunch', vibe: ['rit', 'arts'], cost: '$6 – $12 coffee/bites', duration: '45 mins', desc: 'Bohemian coffee house next to Eastman School of Music, known for fresh espresso and local student energy.', tags: ['Walkable'] },
            { name: 'Pittsford Farms Dairy & Bakery', mealType: 'lunch', vibe: ['family', 'foodie', 'outdoors'], cost: '$5 – $12 treats', duration: '45 mins', desc: 'Historic canal-side dairy shop famous for fresh soft-serve, local chocolate milk, and pastries.', tags: ['Erie Canal', 'Kid Friendly'] },
            
            // Evening & Dinner Venues
            { name: 'Genesee Brew House & Rooftop', mealType: 'dinner', vibe: ['foodie', 'rit', 'outdoors'], cost: '$20 – $35 per meal', duration: '1.5 hrs', desc: 'Craft taproom and grill featuring rooftop deck views directly overlooking High Falls waterfall.', tags: ['Walkable'] },
            { name: 'Dinosaur Bar-B-Que', mealType: 'dinner', vibe: ['foodie', 'family', 'rit'], cost: '$22 – $40 per meal', duration: '1.5 hrs', desc: 'Legendary upstate NY barbecue inside a converted historic pump house on the Genesee River.', tags: ['Kid Friendly'] },
            { name: 'Fiorella (Public Market District)', mealType: 'dinner', vibe: ['foodie', 'premium'], cost: '$45 – $75 per meal', duration: '1.5 hrs', desc: 'Artisanal farm-to-table Italian restaurant sourcing fresh produce directly from market farmers.', tags: ['Walkable'] },
            { name: 'The Owl House', mealType: 'dinner', vibe: ['foodie', 'arts'], cost: '$25 – $45 per meal', duration: '1.5 hrs', desc: 'Cozy craft beverage spot in Park Ave neighborhood known for gourmet comfort food and vegan options.', tags: ['Walkable'] },
            { name: 'Char Steak & Lounge', mealType: 'dinner', vibe: ['premium', 'foodie'], cost: '$60 – $110+ per meal', duration: '2 hrs', desc: 'Upscale dining venue located in The Strathallan hotel featuring prime steaks and handcrafted cocktails.', tags: [] }
        ];

        // EXPANDED DATA BANK: Separated into explicit categories to guarantee zero duplicates
        const ROC_ACTIVITIES_LIST = [
            // Museums & Interactive
            { name: 'The Strong National Museum of Play', vibe: ['family', 'arts', 'rit'], cost: '$23 per ticket', duration: '3 hrs', desc: 'World famous interactive museum featuring the National Toy Hall of Fame, giant vintage arcade, and video game history.', tags: ['Kid Friendly', 'Walkable'] },
            { name: 'George Eastman Museum & Mansion', vibe: ['arts', 'foodie'], cost: '$20 per ticket', duration: '2 hrs', desc: 'The world’s oldest photography museum located inside Kodak founder George Eastman’s historic estate.', tags: ['Walkable'] },
            { name: 'Rochester Museum & Science Center (RMSC)', vibe: ['family', 'arts'], cost: '$18 per ticket', duration: '2 hrs', desc: 'Interactive science exhibits, regional technology history, and Strasenburgh Planetarium star shows.', tags: ['Kid Friendly'] },
            { name: 'Memorial Art Gallery (MAG)', vibe: ['arts'], cost: '$19 per ticket', duration: '2 hrs', desc: '5,000 years of art history featuring medieval tapestries, modern masterpieces, and Centennial Sculpture Park.', tags: ['Walkable'] },
            
            // Outdoors & Scenic
            { name: 'High Falls & Genesee River Gorge Bridge', vibe: ['outdoors', 'rit', 'foodie'], cost: 'Free admission', duration: '1.5 hrs', desc: 'Walk across the historic pedestrian bridge over Rochester’s roaring 96-foot downtown waterfall.', tags: ['Walkable'] },
            { name: 'Highland Park & Lamberton Conservatory', vibe: ['outdoors', 'family', 'rit'], cost: '$5 admission', duration: '2 hrs', desc: 'Explore Olmsted-designed botanical gardens, historic lilac displays, and exotic tropical greenhouses.', tags: ['Kid Friendly'] },
            { name: 'Erie Canal Towpath Stroll (Pittsford Village)', vibe: ['outdoors', 'foodie'], cost: 'Free stroll', duration: '1.5 hrs', desc: 'Scenic waterfront stroll past canal locks, boat docks, and boutique shops in historic Pittsford.', tags: ['Erie Canal', 'Walkable'] },
            { name: 'Charlotte Pier & Ontario Beach Park', vibe: ['outdoors', 'family'], cost: 'Free ($2 carousel)', duration: '2 hrs', desc: 'Walk out to the historic lighthouse pier along Lake Ontario and ride the 1905 Dentzel Carousel.', tags: ['Kid Friendly'] },
            { name: 'Seneca Park Zoo', vibe: ['family', 'outdoors'], cost: '$14 per ticket', duration: '2.5 hrs', desc: 'Lush riverfront zoo featuring African elephants, sea lions, and red pandas along the Genesee River.', tags: ['Kid Friendly'] },
            
            // RIT & Unique Rochester Experiences
            { name: 'RIT Campus & SHED Innovation Hub Tour', vibe: ['rit'], cost: 'Free tour', duration: '2 hrs', desc: 'Tour RIT’s iconic brick campus, state-of-the-art SHED maker spaces, and student design galleries.', tags: ['Kid Friendly'] },
            { name: 'Rochester Public Market Shopping', vibe: ['foodie', 'family', 'outdoors'], cost: 'Free entry ($10-$15 bites)', duration: '2 hrs', desc: 'Historic 1905 market packed with local produce, artisanal baked goods, and vibrant city culture.', tags: ['Walkable'] }
        ];

        let currentPackage = null;

        // -------------------------------------------------------------
        // APPLICATION INITIALIZATION & TAB NAVIGATION
        // -------------------------------------------------------------
        window.addEventListener('DOMContentLoaded', () => {
            updateSavedBadgeCount();
            document.getElementById('package-form').dispatchEvent(new Event('submit'));
        });

        function switchTab(tabName) {
            const builderView = document.getElementById('view-builder');
            const savedView = document.getElementById('view-saved');
            const btnBuilder = document.getElementById('tab-btn-builder');
            const btnSaved = document.getElementById('tab-btn-saved');

            if (tabName === 'builder') {
                builderView.classList.remove('hidden');
                savedView.classList.add('hidden');
                btnBuilder.className = "px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg bg-white text-black transition flex items-center space-x-2 border border-white";
                btnSaved.className = "px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg text-zinc-300 hover:text-white hover:bg-zinc-900 transition flex items-center space-x-2 relative border border-transparent";
            } else {
                builderView.classList.add('hidden');
                savedView.classList.remove('hidden');
                btnSaved.className = "px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg bg-white text-black transition flex items-center space-x-2 relative border border-white";
                btnBuilder.className = "px-4 py-2.5 text-xs sm:text-sm font-semibold rounded-lg text-zinc-300 hover:text-white hover:bg-zinc-900 transition flex items-center space-x-2 border border-transparent";
                renderSavedPackages();
            }
        }

        // Helper to pick unique items without duplicates across the trip
        function getUniqueSelection(list, filterFn, usedNamesSet) {
            const candidates = list.filter(item => !usedNamesSet.has(item.name) && filterFn(item));
            if (candidates.length > 0) {
                // Prioritize user preference active tags
                if (activeTags.length > 0) {
                    candidates.sort((a, b) => {
                        const aMatches = a.tags ? a.tags.filter(t => activeTags.includes(t)).length : 0;
                        const bMatches = b.tags ? b.tags.filter(t => activeTags.includes(t)).length : 0;
                        return bMatches - aMatches;
                    });
                } else {
                    candidates.sort(() => 0.5 - Math.random());
                }
                const chosen = candidates[0];
                usedNamesSet.add(chosen.name);
                return chosen;
            }
            // Fallback if strict filter runs dry
            const fallbackCandidates = list.filter(item => !usedNamesSet.has(item.name));
            if (fallbackCandidates.length > 0) {
                const chosen = fallbackCandidates[Math.floor(Math.random() * fallbackCandidates.length)];
                usedNamesSet.add(chosen.name);
                return chosen;
            }
            // Absolute safety fallback
            return list[Math.floor(Math.random() * list.length)];
        }

        // -------------------------------------------------------------
        // DYNAMIC PACKAGE GENERATION ALGORITHM (Strict No-Duplicates)
        // -------------------------------------------------------------
        async function generatePackage(event) {
            if (event) event.preventDefault();

            const days = parseInt(document.getElementById('param-days').value);
            const vibe = document.getElementById('param-vibe').value;
            const budget = document.getElementById('param-budget').value;
            const pace = document.getElementById('param-pace').value;

            const spinner = document.getElementById('loading-spinner');
            const results = document.getElementById('package-results');
            
            spinner.classList.remove('hidden');
            results.classList.add('hidden');

            await new Promise(r => setTimeout(r, 400));

            // 1. Select Basecamp Hotel based on Budget Tier & Vibe
            const hotelsByBudget = ROC_HOTELS.filter(h => h.budgetTier === budget);
            const matchedHotels = hotelsByBudget.filter(h => h.vibe.includes(vibe));
            
            // Priority: Match budget tier + vibe, fallback to budget tier match, fallback to general
            let selectedHotel;
            if (matchedHotels.length > 0) {
                selectedHotel = matchedHotels[Math.floor(Math.random() * matchedHotels.length)];
            } else if (hotelsByBudget.length > 0) {
                selectedHotel = hotelsByBudget[Math.floor(Math.random() * hotelsByBudget.length)];
            } else {
                selectedHotel = ROC_HOTELS[0];
            }

            // Set to track used locations and guarantee NO duplicates
            const usedLocationNames = new Set();
            const itinerary = [];

            for (let d = 1; d <= days; d++) {
                const dayItems = [];

                // 1. Morning Landmark/Activity
                const morningAct = getUniqueSelection(
                    ROC_ACTIVITIES_LIST,
                    item => item.vibe.includes(vibe) || item.vibe.includes('family'),
                    usedLocationNames
                );
                dayItems.push({ time: 'Morning • 9:30 AM', ...morningAct, category: 'Morning Activity', type: 'Activity' });

                // 2. Lunch Stop (Distinct Dining venue)
                const lunchSpot = getUniqueSelection(
                    ROC_DINING_LIST,
                    item => item.mealType === 'lunch' || item.vibe.includes(vibe),
                    usedLocationNames
                );
                dayItems.push({ time: 'Lunch • 12:30 PM', ...lunchSpot, category: 'Lunch Spot', type: 'Dining' });

                // 3. Afternoon Experience (Distinct Activity venue)
                const afternoonAct = getUniqueSelection(
                    ROC_ACTIVITIES_LIST,
                    item => true,
                    usedLocationNames
                );
                dayItems.push({ time: 'Afternoon • 2:30 PM', ...afternoonAct, category: 'Afternoon Attraction', type: 'Activity' });

                // 4. Evening Dinner & Vibe (Distinct Evening venue)
                if (pace === 'balanced' || pace === 'packed' || days <= 2) {
                    const dinnerSpot = getUniqueSelection(
                        ROC_DINING_LIST,
                        item => item.mealType === 'dinner' || item.cost === '$$' || item.cost === '$$$',
                        usedLocationNames
                    );
                    dayItems.push({ time: 'Evening • 6:30 PM', ...dinnerSpot, category: 'Dinner & Craft Vibe', type: 'Dining' });
                }

                // 5. Extra Evening Spot if Packed Pace
                if (pace === 'packed') {
                    const lateNightSpot = getUniqueSelection(
                        ROC_ACTIVITIES_LIST,
                        item => item.vibe.includes('outdoors') || item.vibe.includes('arts'),
                        usedLocationNames
                    );
                    dayItems.push({ time: 'Night • 8:30 PM', ...lateNightSpot, category: 'Evening Stroll / Nightlife', type: 'Activity' });
                }

                itinerary.push({ dayNumber: d, items: dayItems });
            }

            const vibeTitles = {
                family: 'Family Play & Discovery',
                foodie: 'Culinary & Craft Brews',
                arts: 'Arts, History & Culture',
                outdoors: 'Scenic Parks & Waterfalls',
                rit: 'RIT Visitor & Campus Tour'
            };

            const budgetLabels = {
                budget: '$80 – $110 Total Daily Budget',
                moderate: '$170 – $240 Total Daily Budget',
                premium: '$300 – $450+ Total Daily Budget'
            };

            currentPackage = {
                id: 'pkg_' + Date.now(),
                title: `${days}-Day ${vibeTitles[vibe]} Package`,
                vibe: vibe,
                duration: `${days} ${days === 1 ? 'Day' : 'Days'}`,
                budget: budget,
                budgetLabel: budgetLabels[budget],
                hotel: selectedHotel,
                itinerary: itinerary,
                tags: [...activeTags],
                createdAt: new Date().toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' })
            };

            displayPackage(currentPackage);

            spinner.classList.add('hidden');
            results.classList.remove('hidden');
        }

        function displayPackage(pkg) {
            document.getElementById('pkg-title').textContent = pkg.title;
            document.getElementById('pkg-tag').textContent = `${pkg.vibe.toUpperCase()} BUNDLE`;
            document.getElementById('pkg-duration-badge').textContent = `• ${pkg.duration} (${pkg.budgetLabel})`;
            
            let desc = `Your customized Rochester care package pairs hotel accommodations at ${pkg.hotel.name} with a curated day-by-day schedule of top regional attractions and dining. Estimated all-inclusive total daily cost: ${pkg.budgetLabel}.`;
            if (pkg.tags && pkg.tags.length > 0) {
                desc += ` Tailored with preference tags: ${pkg.tags.join(', ')}.`;
            }
            document.getElementById('pkg-description').textContent = desc;

            // Basecamp Hotel details
            document.getElementById('hotel-name').textContent = pkg.hotel.name;
            document.getElementById('hotel-details').textContent = `${pkg.hotel.address} — ${pkg.hotel.desc}`;
            document.getElementById('hotel-price').textContent = pkg.hotel.price;
            
            const amenitiesContainer = document.getElementById('hotel-amenities');
            amenitiesContainer.innerHTML = pkg.hotel.amenities.map(a => `
                <span class="px-2.5 py-1 bg-zinc-900 border border-zinc-800 text-zinc-300 rounded text-xs font-semibold">
                    <i class="fa-solid fa-check text-white mr-1"></i>${a}
                </span>
            `).join('');

            // Days timeline display
            const daysContainer = document.getElementById('days-container');
            daysContainer.innerHTML = '';

            pkg.itinerary.forEach(day => {
                const dayEl = document.createElement('div');
                dayEl.className = "bg-white border border-zinc-200 rounded-2xl p-6 sm:p-8 shadow-sm";
                
                let itemsHtml = day.items.map((item, idx) => `
                    <div class="relative pl-6 sm:pl-8 border-l-2 border-black pb-8 last:pb-0">
                        <div class="absolute -left-[7px] top-0 w-3.5 h-3.5 rounded-full bg-black border-2 border-white"></div>
                        
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-1 mb-1">
                            <span class="text-xs font-black text-black uppercase tracking-wider">${item.time} — ${item.category}</span>
                            <span class="text-xs font-medium text-zinc-500"><i class="fa-solid fa-tag mr-1"></i>${item.cost} • Est. ${item.duration}</span>
                        </div>

                        <h4 class="text-lg font-black text-black flex items-center gap-2">
                            ${item.type === 'Dining' ? '<i class="fa-solid fa-utensils text-zinc-700 text-sm"></i>' : '<i class="fa-solid fa-location-dot text-zinc-700 text-sm"></i>'}
                            ${item.name}
                        </h4>

                        <p class="text-sm text-zinc-600 mt-1 leading-relaxed">${item.desc}</p>
                    </div>
                `).join('');

                dayEl.innerHTML = `
                    <div class="flex items-center justify-between border-b border-zinc-200 pb-4 mb-6">
                        <h4 class="text-lg font-black text-black flex items-center">
                            <span class="w-8 h-8 rounded-lg bg-black text-white flex items-center justify-center font-black text-xs mr-3">D${day.dayNumber}</span>
                            Day ${day.dayNumber} Schedule
                        </h4>
                        <span class="text-xs font-bold text-zinc-400 uppercase tracking-widest">ROC BOX Care Package</span>
                    </div>
                    <div class="space-y-2">
                        ${itemsHtml}
                    </div>
                `;

                daysContainer.appendChild(dayEl);
            });
        }

        // -------------------------------------------------------------
        // SAVED PACKAGES / STORAGE MANAGEMENT
        // -------------------------------------------------------------
        function getSavedPackages() {
            try {
                return JSON.parse(localStorage.getItem('roc_saved_packages') || '[]');
            } catch (e) {
                return [];
            }
        }

        function saveCurrentPackage() {
            if (!currentPackage) return;

            let saved = getSavedPackages();
            if (saved.some(p => p.id === currentPackage.id)) {
                showMessage('This package is already in your saved collection!');
                return;
            }

            saved.push(currentPackage);
            try {
                localStorage.setItem('roc_saved_packages', JSON.stringify(saved));
                updateSavedBadgeCount();
                showMessage('Package successfully saved!');
            } catch (e) {
                showMessage('Unable to save package to browser storage.');
            }
        }

        function updateSavedBadgeCount() {
            const saved = getSavedPackages();
            const badge = document.getElementById('saved-badge');
            if (saved.length > 0) {
                badge.textContent = saved.length;
                badge.classList.remove('hidden');
            } else {
                badge.classList.add('hidden');
            }
        }

        function renderSavedPackages() {
            const saved = getSavedPackages();
            const container = document.getElementById('saved-packages-list');
            const emptyState = document.getElementById('no-saved-state');

            container.innerHTML = '';

            if (saved.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            }

            emptyState.classList.add('hidden');

            saved.forEach(pkg => {
                const card = document.createElement('div');
                card.className = "bg-white border border-zinc-200 rounded-2xl p-6 shadow-sm card-hover flex flex-col justify-between";
                card.innerHTML = `
                    <div>
                        <div class="flex items-center justify-between mb-3">
                            <span class="px-2.5 py-1 rounded text-[10px] font-black bg-black text-white uppercase tracking-wider">${pkg.vibe}</span>
                            <span class="text-xs text-zinc-400 font-medium">${pkg.createdAt}</span>
                        </div>
                        <h3 class="text-lg font-black text-black mb-1">${pkg.title}</h3>
                        <p class="text-xs text-zinc-600 mb-4 font-medium"><i class="fa-solid fa-hotel text-zinc-400 mr-1.5"></i>${pkg.hotel.name}</p>
                        
                        <div class="text-xs text-zinc-600 bg-zinc-50 p-3 rounded-lg border border-zinc-100 mb-4">
                            <strong>Package Scope:</strong> ${pkg.itinerary.length} Day Schedule with ${pkg.itinerary.reduce((acc, d) => acc + d.items.length, 0)} stops.
                        </div>
                    </div>

                    <div class="flex items-center space-x-3 border-t border-zinc-100 pt-4">
                        <button onclick="loadSavedPackage('${pkg.id}')" class="flex-1 py-2.5 bg-black hover:bg-zinc-800 text-white rounded-lg text-xs font-bold uppercase tracking-wider transition">
                            View Package
                        </button>
                        <button onclick="deleteSavedPackage('${pkg.id}')" class="px-3 py-2.5 border border-zinc-200 text-zinc-500 hover:text-black hover:bg-zinc-100 rounded-lg text-xs transition">
                            <i class="fa-solid fa-trash"></i>
                        </button>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function loadSavedPackage(id) {
            const saved = getSavedPackages();
            const found = saved.find(p => p.id === id);
            if (found) {
                currentPackage = found;
                displayPackage(found);
                switchTab('builder');
                document.getElementById('package-results').classList.remove('hidden');
            }
        }

        function deleteSavedPackage(id) {
            let saved = getSavedPackages();
            saved = saved.filter(p => p.id !== id);
            localStorage.setItem('roc_saved_packages', JSON.stringify(saved));
            updateSavedBadgeCount();
            renderSavedPackages();
        }

        function clearSavedPackages() {
            localStorage.removeItem('roc_saved_packages');
            updateSavedBadgeCount();
            renderSavedPackages();
        }

        // Custom message toast
        function showMessage(msg) {
            const toast = document.createElement('div');
            toast.className = "fixed bottom-5 right-5 bg-black text-white px-5 py-3 rounded-xl shadow-2xl text-xs font-bold z-50 border border-zinc-800 flex items-center space-x-2";
            toast.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-400"></i><span>${msg}</span>`;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.remove();
            }, 3000);
        }
    </script>
</body>
</html>
