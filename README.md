```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Canvas & Ink | Unapologetic Creativity</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Playfair+Display:ital,wght@0,600;1,400&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fdf2f8',
                            100: '#fce7f3',
                            500: '#ec4899',
                            600: '#db2777',
                            700: '#be185d',
                            900: '#831843',
                        },
                        darkbg: '#0b0f17',
                        darkcard: '#151c28',
                        darkborder: '#222f43'
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                        serif: ['Playfair Display', 'serif'],
                    }
                }
            }
        }
    </script>
    <style>
        .glass-panel {
            background: rgba(21, 28, 40, 0.7);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .glass-light {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(0, 0, 0, 0.05);
        }
        .gradient-text {
            background: linear-gradient(135deg, #ec4899 0%, #8b5cf6 50%, #3b82f6 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gradient-btn {
            background: linear-gradient(135deg, #ec4899 0%, #8b5cf6 100%);
            transition: all 0.3s ease;
        }
        .gradient-btn:hover {
            box-shadow: 0 10px 25px -5px rgba(236, 72, 153, 0.5);
            transform: translateY(-2px);
        }
        .masonry-grid {
            columns: 1;
        }
        @media (min-width: 640px) { .masonry-grid { columns: 2; } }
        @media (min-width: 1024px) { .masonry-grid { columns: 3; } }
        .masonry-item {
            break-inside: avoid;
            margin-bottom: 1.5rem;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0b0f17;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f293d;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #ec4899;
        }
    </style>
</head>
<body class="bg-darkbg text-slate-100 font-sans antialiased min-h-screen flex flex-col selection:bg-brand-500 selection:text-white">

    <!-- Navigation Header -->
    <header class="sticky top-0 z-40 w-full glass-panel border-b border-slate-800/80 transition-all duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="scrollToTop()">
                <div class="w-10 h-10 rounded-xl gradient-btn flex items-center justify-center text-white font-serif text-xl font-bold shadow-lg shadow-brand-500/20">
                    C&I
                </div>
                <div>
                    <span class="text-xl font-extrabold tracking-tight gradient-text">Canvas & Ink</span>
                    <span class="hidden sm:inline-block text-xs text-slate-400 font-medium ml-2 px-2 py-0.5 rounded-full bg-slate-800 border border-slate-700">DU Creator Edition</span>
                </div>
            </div>

            <!-- Header Actions -->
            <div class="flex items-center space-x-3 sm:space-x-4">
                <button onclick="toggleSubmitModal(true)" class="gradient-btn text-white text-sm sm:text-base font-semibold px-4 sm:px-5 py-2.5 rounded-xl flex items-center space-x-2 shadow-lg">
                    <i class="fa-solid fa-plus text-xs"></i>
                    <span>Share Work</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Hero Banner -->
    <section class="relative overflow-hidden pt-12 pb-16 sm:pt-20 sm:pb-24 border-b border-slate-800/50 bg-gradient-to-b from-slate-900/50 to-transparent">
        <div class="absolute inset-0 z-0 opacity-20 bg-[radial-gradient(#ec4899_1px,transparent_1px)] [background-size:24px_24px]"></div>
        
        <div class="relative z-10 max-w-5xl mx-auto px-4 text-center">
            <div class="inline-flex items-center space-x-2 px-4 py-2 rounded-full bg-brand-500/10 border border-brand-500/20 text-brand-500 text-xs sm:text-sm font-semibold mb-6 animate-pulse">
                <i class="fa-solid fa-bolt"></i>
                <span>Zero Budget • Pure Passion • Built by Students</span>
            </div>
            
            <h1 class="text-4xl sm:text-6xl lg:text-7xl font-extrabold tracking-tight mb-6 leading-tight">
                Where Raw Ideas Find Their <span class="serif italic font-normal gradient-text">Audience.</span>
            </h1>
            
            <p class="text-slate-400 text-lg sm:text-xl max-w-2xl mx-auto mb-8 font-light leading-relaxed">
                No algorithms. No paywalls. Just an open digital space for Delhi University students & independent creators to display poems, sketches, thoughts, and digital art.
            </p>

            <!-- Quick Stats / Badges -->
            <div class="flex flex-wrap justify-center items-center gap-6 text-slate-400 text-xs sm:text-sm font-medium pt-4">
                <div class="flex items-center space-x-2 bg-slate-800/60 px-4 py-2 rounded-lg border border-slate-700/50">
                    <i class="fa-solid fa-feather-pointed text-brand-500"></i>
                    <span id="stat-poems">0 Poems Shared</span>
                </div>
                <div class="flex items-center space-x-2 bg-slate-800/60 px-4 py-2 rounded-lg border border-slate-700/50">
                    <i class="fa-solid fa-palette text-purple-400"></i>
                    <span id="stat-art">0 Art Pieces</span>
                </div>
                <div class="flex items-center space-x-2 bg-slate-800/60 px-4 py-2 rounded-lg border border-slate-700/50">
                    <i class="fa-solid fa-heart text-rose-500"></i>
                    <span id="stat-likes">0 Total Loves</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Main Gallery & Feed -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-10">
        
        <!-- Controls Bar: Search & Category Filter -->
        <div class="flex flex-col sm:flex-row items-center justify-between gap-4 mb-8">
            <!-- Filter Tabs -->
            <div class="flex items-center space-x-2 bg-slate-900/80 p-1.5 rounded-2xl border border-slate-800 w-full sm:w-auto overflow-x-auto">
                <button onclick="setFilter('all')" id="filter-all" class="filter-btn active px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold transition-all duration-200 bg-brand-600 text-white shadow-md">
                    ✨ All Works
                </button>
                <button onclick="setFilter('Poem')" id="filter-poem" class="filter-btn px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-slate-400 hover:text-white transition-all duration-200">
                    ✍️ Poems & Prose
                </button>
                <button onclick="setFilter('Artwork')" id="filter-artwork" class="filter-btn px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-slate-400 hover:text-white transition-all duration-200">
                    🎨 Visual Art
                </button>
                <button onclick="setFilter('Thought')" id="filter-thought" class="filter-btn px-4 py-2 rounded-xl text-xs sm:text-sm font-semibold text-slate-400 hover:text-white transition-all duration-200">
                    💡 Thoughts
                </button>
            </div>

            <!-- Search Bar -->
            <div class="relative w-full sm:w-72">
                <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-500 text-sm"></i>
                <input type="text" id="searchInput" oninput="handleSearch()" placeholder="Search creator or title..." class="w-full pl-10 pr-4 py-2.5 bg-slate-900/80 border border-slate-800 rounded-xl text-sm focus:outline-none focus:border-brand-500 text-slate-200 placeholder-slate-500 transition-colors">
            </div>
        </div>

        <!-- Masonry Feed Container -->
        <div id="gallery" class="masonry-grid gap-6">
            <!-- Dynamic Post Cards will be injected here -->
        </div>

        <!-- Empty State Container -->
        <div id="emptyState" class="hidden text-center py-20 bg-slate-900/30 border border-dashed border-slate-800 rounded-3xl my-6">
            <div class="w-16 h-16 bg-slate-800/80 text-brand-500 rounded-2xl flex items-center justify-center mx-auto mb-4 text-2xl">
                <i class="fa-solid fa-ghost"></i>
            </div>
            <h3 class="text-xl font-bold text-slate-200 mb-2">No creations found</h3>
            <p class="text-slate-400 text-sm max-w-sm mx-auto mb-6">Be the first to leave your mark in this category!</p>
            <button onclick="toggleSubmitModal(true)" class="gradient-btn text-white text-sm font-semibold px-5 py-2.5 rounded-xl shadow-lg">
                Publish a Creation
            </button>
        </div>
    </main>

    <!-- Footer -->
    <footer class="mt-auto border-t border-slate-800/80 bg-slate-950/80 py-10 text-slate-400 text-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="flex items-center space-x-3">
                <div class="w-7 h-7 rounded-lg gradient-btn flex items-center justify-center text-white font-serif text-xs font-bold">
                    C&I
                </div>
                <span class="font-semibold text-slate-300">Canvas & Ink</span>
                <span class="text-xs text-slate-500">| Designed for non-stop growth</span>
            </div>
            <p class="text-xs text-slate-500 text-center sm:text-right">
                Built with 💖 using zero budget. Proving that skills speak louder than money.
            </p>
        </div>
    </footer>

    <!-- Submission Modal -->
    <div id="submitModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-sm opacity-0 pointer-events-none transition-all duration-300">
        <div class="bg-darkcard border border-darkborder w-full max-w-xl rounded-3xl shadow-2xl p-6 sm:p-8 transform scale-95 transition-all duration-300 relative overflow-hidden" id="modalBox">
            <!-- Modal Header -->
            <div class="flex items-center justify-between mb-6 pb-4 border-b border-slate-800">
                <div>
                    <h2 class="text-2xl font-extrabold text-white">Share Your Creation</h2>
                    <p class="text-xs text-slate-400 mt-1">Express yourself freely without worrying about judgment.</p>
                </div>
                <button onclick="toggleSubmitModal(false)" class="w-9 h-9 rounded-full bg-slate-800 text-slate-400 hover:text-white flex items-center justify-center transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Form -->
            <form id="submissionForm" onsubmit="handleFormSubmit(event)" class="space-y-5">
                <div>
                    <label class="block text-xs font-semibold uppercase text-slate-400 mb-2">Creator Name / Alias *</label>
                    <input type="text" id="author" required placeholder="e.g. Sahil, DU Poet, or Anonymous" class="w-full px-4 py-3 bg-slate-900 border border-slate-800 rounded-xl text-sm text-slate-200 focus:outline-none focus:border-brand-500 transition-colors">
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-semibold uppercase text-slate-400 mb-2">Category *</label>
                        <select id="type" onchange="toggleContentFormat()" class="w-full px-4 py-3 bg-slate-900 border border-slate-800 rounded-xl text-sm text-slate-200 focus:outline-none focus:border-brand-500 transition-colors">
                            <option value="Poem">✍️ Poem / Short Story</option>
                            <option value="Artwork">🎨 Artwork / Digital Design</option>
                            <option value="Thought">💡 Thought / Musings</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold uppercase text-slate-400 mb-2">Work Title *</label>
                        <input type="text" id="title" required placeholder="e.g. Midnight Thoughts" class="w-full px-4 py-3 bg-slate-900 border border-slate-800 rounded-xl text-sm text-slate-200 focus:outline-none focus:border-brand-500 transition-colors">
                    </div>
                </div>

                <!-- Text or Image URL Area -->
                <div id="textInputContainer">
                    <label class="block text-xs font-semibold uppercase text-slate-400 mb-2">Your Words / Lines *</label>
                    <textarea id="textContent" rows="5" placeholder="Write your poem, quote or thought here..." class="w-full px-4 py-3 bg-slate-900 border border-slate-800 rounded-xl text-sm text-slate-200 focus:outline-none focus:border-brand-500 transition-colors font-serif"></textarea>
                </div>

                <div id="imageInputContainer" class="hidden">
                    <label class="block text-xs font-semibold uppercase text-slate-400 mb-2">Image Link (URL) *</label>
                    <input type="url" id="imageUrl" placeholder="https://images.unsplash.com/photo-..." class="w-full px-4 py-3 bg-slate-900 border border-slate-800 rounded-xl text-sm text-slate-200 focus:outline-none focus:border-brand-500 transition-colors">
                    <p class="text-[11px] text-slate-500 mt-1">Tip: Paste a direct image URL from Unsplash, Imgur, or Pinterest.</p>
                </div>

                <!-- Submit Button -->
                <div class="pt-2">
                    <button type="submit" class="w-full gradient-btn text-white font-bold py-3.5 rounded-xl shadow-lg flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-paper-plane text-sm"></i>
                        <span>Publish to Community</span>
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 bg-slate-800 border border-brand-500/50 text-slate-100 px-5 py-3 rounded-2xl shadow-2xl flex items-center space-x-3 pointer-events-none">
        <div class="w-8 h-8 rounded-full bg-brand-500/20 text-brand-500 flex items-center justify-center font-bold">
            <i class="fa-solid fa-check text-xs"></i>
        </div>
        <span id="toastMsg" class="text-sm font-medium">Work published successfully!</span>
    </div>

    <!-- Script Engine -->
    <script>
        // Default Starter Feed Data
        const initialCreations = [
            {
                id: 1,
                author: "Ananya Sharma",
                type: "Poem",
                title: "Chai & North Campus Fog",
                content: "Between the lecture halls and tea stalls,\nWhere silent ambition quietly crawls.\nWe trade our dreams for cupfuls of steam,\nLiving life larger than it might seem.",
                likes: 34,
                timestamp: "2 hours ago"
            },
            {
                id: 2,
                author: "Rohan V.",
                type: "Artwork",
                title: "Monochrome Solitude",
                content: "https://images.unsplash.com/photo-1579783900882-c0d3dad7b119?auto=format&fit=crop&w=800&q=80",
                likes: 58,
                timestamp: "5 hours ago"
            },
            {
                id: 3,
                author: "Anonymous",
                type: "Thought",
                title: "Zero Budget Reality",
                content: "Having no money isn't a barrier. It forces you to get creative, learn coding, and build things yourself.",
                likes: 89,
                timestamp: "1 day ago"
            },
            {
                id: 4,
                author: "Priya M.",
                type: "Artwork",
                title: "Color Burst",
                content: "https://images.unsplash.com/photo-1541701494587-cb58502866ab?auto=format&fit=crop&w=800&q=80",
                likes: 42,
                timestamp: "2 days ago"
            }
        ];

        let currentFilter = 'all';
        let searchQuery = '';

        // Initialize Local Storage or Default Posts
        function getCreations() {
            const stored = localStorage.getItem('canvas_ink_creations');
            return stored ? JSON.parse(stored) : initialCreations;
        }

        function saveCreations(data) {
            localStorage.setItem('canvas_ink_creations', JSON.stringify(data));
            updateStats();
        }

        // Render Posts to Grid
        function renderGallery() {
            const gallery = document.getElementById('gallery');
            const emptyState = document.getElementById('emptyState');
            const creations = getCreations();

            const filtered = creations.filter(item => {
                const matchesCategory = currentFilter === 'all' || item.type === currentFilter;
                const matchesSearch = item.title.toLowerCase().includes(searchQuery.toLowerCase()) || 
                                      item.author.toLowerCase().includes(searchQuery.toLowerCase()) ||
                                      item.content.toLowerCase().includes(searchQuery.toLowerCase());
                return matchesCategory && matchesSearch;
            });

            if (filtered.length === 0) {
                gallery.innerHTML = '';
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            gallery.innerHTML = filtered.map(item => {
                let bodyHtml = '';
                if (item.type === 'Artwork') {
                    bodyHtml = `
                        <div class="overflow-hidden rounded-2xl mb-4 bg-slate-900 border border-slate-800">
                            <img src="${item.content}" alt="${item.title}" class="w-full h-auto object-cover hover:scale-105 transition-transform duration-500" onerror="this.onerror=null; this.src='https://images.unsplash.com/photo-1579783900882-c0d3dad7b119?auto=format&fit=crop&w=800&q=80';">
                        </div>`;
                } else if (item.type === 'Poem') {
                    bodyHtml = `
                        <p class="text-slate-300 font-serif whitespace-pre-line text-sm sm:text-base leading-relaxed mb-4 italic pl-3 bo
