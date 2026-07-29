<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToolVerse AI | All-in-One Multi-Tool Platform</title>
    <meta name="description" content="300+ Professional AI, Text, Image, and Developer tools in one place.">
    
    <!-- External Dependencies -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#6366f1',
                        secondary: '#a855f7',
                        dark: '#0f172a',
                    },
                    backdropBlur: {
                        xs: '2px',
                    }
                }
            }
        }
    </script>

    <style>
        body { font-family: 'Inter', sans-serif; transition: background-color 0.3s ease; }
        .glass { background: rgba(255, 255, 255, 0.7); backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2); }
        .dark .glass { background: rgba(15, 23, 42, 0.8); border: 1px solid rgba(255, 255, 255, 0.1); }
        .tool-card:hover { transform: translateY(-5px); transition: all 0.3s ease; }
        .custom-scrollbar::-webkit-scrollbar { width: 6px; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #6366f1; border-radius: 10px; }
        #page-loader { position: fixed; inset: 0; z-index: 9999; background: white; display: flex; align-items: center; justify-content: center; transition: opacity 0.5s; }
        .dark #page-loader { background: #0f172a; }
        .hidden-section { display: none; }
    </style>
</head>
<body class="bg-gray-50 text-gray-900 dark:bg-dark dark:text-gray-100 min-h-screen">

    <!-- Page Loader -->
    <div id="page-loader">
        <div class="animate-spin rounded-full h-16 w-16 border-t-4 border-primary"></div>
    </div>

    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 glass border-b">
        <div class="container mx-auto px-4 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2 cursor-pointer" onclick="navigateTo('home')">
                <div class="bg-primary p-2 rounded-lg text-white">
                    <i class="fas fa-microchip text-xl"></i>
                </div>
                <span class="text-xl font-bold tracking-tight">ToolVerse<span class="text-primary">AI</span></span>
            </div>

            <div class="hidden md:flex items-center gap-6">
                <a href="#categories" class="hover:text-primary transition" onclick="navigateTo('home')">Categories</a>
                <button onclick="navigateTo('admin')" class="hover:text-primary">Admin</button>
                <div id="auth-buttons" class="flex items-center gap-4">
                    <button onclick="navigateTo('login')" class="px-4 py-2 hover:text-primary">Login</button>
                    <button onclick="navigateTo('login')" class="bg-primary text-white px-5 py-2 rounded-full text-sm font-semibold shadow-lg hover:opacity-90 transition">Join Free</button>
                </div>
                <button id="theme-toggle" class="p-2 rounded-full hover:bg-gray-200 dark:hover:bg-gray-700 transition">
                    <i class="fas fa-moon dark:hidden"></i>
                    <i class="fas fa-sun hidden dark:block"></i>
                </button>
            </div>
            
            <button class="md:hidden text-2xl" onclick="toggleMobileMenu()">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="fixed inset-0 z-40 bg-white dark:bg-dark hidden pt-20 px-6">
        <div class="flex flex-col gap-6 text-xl">
            <a href="#" onclick="navigateTo('home'); toggleMobileMenu()">Home</a>
            <a href="#" onclick="navigateTo('home'); toggleMobileMenu()">Tools</a>
            <a href="#" onclick="navigateTo('admin'); toggleMobileMenu()">Admin Dashboard</a>
            <a href="#" onclick="navigateTo('login'); toggleMobileMenu()">Account</a>
            <hr>
            <button id="mobile-theme-toggle" class="text-left">Toggle Theme</button>
        </div>
    </div>

    <!-- MAIN CONTENT AREA -->
    <main class="pt-24 pb-12">
        
        <!-- HOME SECTION -->
        <section id="home-section" class="container mx-auto px-4">
            <!-- Hero -->
            <div class="text-center max-w-3xl mx-auto mb-16">
                <h1 class="text-4xl md:text-6xl font-extrabold mb-6 leading-tight">
                    Every Tool You Need, <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-secondary">Powered by AI.</span>
                </h1>
                <p class="text-gray-500 dark:text-gray-400 text-lg mb-8">
                    Optimize images, format code, count words, and generate content. 300+ tools for developers, creators, and students.
                </p>
                <div class="relative max-w-xl mx-auto">
                    <i class="fas fa-search absolute left-4 top-1/2 -translate-y-1/2 text-gray-400"></i>
                    <input type="text" id="tool-search" placeholder="Search 300+ tools (e.g. JSON, BMI, Image)..." 
                        class="w-full pl-12 pr-4 py-4 rounded-2xl border dark:bg-gray-800 dark:border-gray-700 focus:ring-2 focus:ring-primary outline-none shadow-xl transition"
                        onkeyup="searchTools(this.value)">
                </div>
            </div>

            <!-- Categories -->
            <div id="categories" class="mb-12">
                <div class="flex items-center justify-between mb-8">
                    <h2 class="text-2xl font-bold">Categories</h2>
                    <div class="flex gap-2" id="category-filters">
                        <!-- Dynamic Filters -->
                    </div>
                </div>
                <div id="tools-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
                    <!-- Dynamic Tools Card -->
                </div>
            </div>

            <!-- Trending / Recent -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-16">
                <div class="glass p-6 rounded-2xl">
                    <h3 class="text-xl font-bold mb-4 flex items-center gap-2">
                        <i class="fas fa-fire text-orange-500"></i> Trending Tools
                    </h3>
                    <div id="trending-list" class="space-y-3"></div>
                </div>
                <div class="glass p-6 rounded-2xl">
                    <h3 class="text-xl font-bold mb-4 flex items-center gap-2">
                        <i class="fas fa-history text-blue-500"></i> Recently Used
                    </h3>
                    <div id="history-list" class="space-y-3"></div>
                </div>
            </div>
        </section>

        <!-- TOOL WORKSPACE SECTION -->
        <section id="tool-section" class="hidden-section container mx-auto px-4 max-w-5xl">
            <button onclick="navigateTo('home')" class="mb-6 flex items-center gap-2 text-gray-500 hover:text-primary transition">
                <i class="fas fa-arrow-left"></i> Back to All Tools
            </button>
            
            <div id="tool-ui-container" class="glass p-6 md:p-10 rounded-3xl shadow-2xl">
                <!-- Dynamic Tool Interface Injected Here -->
            </div>
        </section>

        <!-- AUTH SECTION -->
        <section id="login-section" class="hidden-section container mx-auto px-4 max-w-md">
            <div class="glass p-8 rounded-3xl shadow-2xl mt-10">
                <h2 class="text-3xl font-bold text-center mb-8">Welcome Back</h2>
                <div class="space-y-4">
                    <div>
                        <label class="block text-sm mb-1">Email</label>
                        <input type="email" placeholder="hello@example.com" class="w-full p-3 rounded-xl border dark:bg-gray-800 dark:border-gray-700 outline-none">
                    </div>
                    <div>
                        <label class="block text-sm mb-1">Password</label>
                        <input type="password" placeholder="••••••••" class="w-full p-3 rounded-xl border dark:bg-gray-800 dark:border-gray-700 outline-none">
                    </div>
                    <button onclick="loginSuccess()" class="w-full bg-primary text-white py-3 rounded-xl font-bold shadow-lg hover:opacity-90 transition">Sign In</button>
                    <p class="text-center text-sm text-gray-500">Don't have an account? <a href="#" class="text-primary font-bold">Sign up</a></p>
                </div>
            </div>
        </section>

        <!-- ADMIN SECTION -->
        <section id="admin-section" class="hidden-section container mx-auto px-4">
            <div class="grid grid-cols-1 lg:grid-cols-4 gap-8">
                <div class="lg:col-span-1 space-y-4">
                    <div class="glass p-6 rounded-2xl">
                        <h3 class="font-bold mb-4">Admin Dashboard</h3>
                        <nav class="space-y-2">
                            <button class="w-full text-left p-2 rounded bg-primary text-white">Analytics</button>
                            <button class="w-full text-left p-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">Manage Tools</button>
                            <button class="w-full text-left p-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">User Control</button>
                            <button class="w-full text-left p-2 rounded hover:bg-gray-100 dark:hover:bg-gray-800">Ad Settings</button>
                        </nav>
                    </div>
                </div>
                <div class="lg:col-span-3 space-y-8">
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <div class="bg-blue-500 p-6 rounded-2xl text-white shadow-lg">
                            <p class="text-blue-100">Total Visits</p>
                            <h4 class="text-3xl font-bold">128,492</h4>
                        </div>
                        <div class="bg-purple-500 p-6 rounded-2xl text-white shadow-lg">
                            <p class="text-purple-100">Active Users</p>
                            <h4 class="text-3xl font-bold">4,120</h4>
                        </div>
                        <div class="bg-green-500 p-6 rounded-2xl text-white shadow-lg">
                            <p class="text-green-100">Ad Revenue</p>
                            <h4 class="text-3xl font-bold">$1,240.50</h4>
                        </div>
                    </div>
                    <div class="glass p-8 rounded-2xl">
                        <h3 class="text-xl font-bold mb-6">Real-time Activity</h3>
                        <div class="space-y-4" id="activity-log">
                            <!-- Simulated log -->
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="border-t py-12 mt-20 dark:border-gray-800">
        <div class="container mx-auto px-4 text-center">
            <div class="flex items-center justify-center gap-2 mb-6">
                <div class="bg-primary p-2 rounded-lg text-white">
                    <i class="fas fa-microchip text-xl"></i>
                </div>
                <span class="text-xl font-bold">ToolVerse<span class="text-primary">AI</span></span>
            </div>
            <p class="text-gray-500 mb-8 max-w-lg mx-auto">Providing high-quality utility tools for everyday digital tasks. 100% free and client-side processing.</p>
            <div class="flex justify-center gap-6 text-2xl text-gray-400 mb-8">
                <i class="fab fa-twitter hover:text-primary cursor-pointer"></i>
                <i class="fab fa-github hover:text-primary cursor-pointer"></i>
                <i class="fab fa-facebook hover:text-primary cursor-pointer"></i>
            </div>
            <div class="text-sm text-gray-500">
                &copy; 2024 ToolVerse AI. All rights reserved. 
            </div>
        </div>
    </footer>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-10 left-1/2 -translate-x-1/2 bg-dark text-white px-6 py-3 rounded-full shadow-2xl opacity-0 translate-y-20 transition duration-300 z-[100]">
        Action Successful!
    </div>

    <script>
        /** 
         * APP STATE & DATABASE
         */
        const state = {
            activeTool: null,
            favorites: JSON.parse(localStorage.getItem('mfai_favs')) || [],
            history: JSON.parse(localStorage.getItem('mfai_history')) || [],
            theme: localStorage.getItem('mfai_theme') || 'light'
        };

        const categories = [
            { id: 'all', name: 'All Tools', icon: 'fa-border-all' },
            { id: 'text', name: 'Text Tools', icon: 'fa-align-left' },
            { id: 'dev', name: 'Developer', icon: 'fa-code' },
            { id: 'calc', name: 'Calculators', icon: 'fa-calculator' },
            { id: 'img', name: 'Images', icon: 'fa-image' },
            { id: 'seo', name: 'SEO', icon: 'fa-search' },
            { id: 'ai', name: 'AI Interface', icon: 'fa-robot' }
        ];

        const tools = [
            // TEXT TOOLS
            { id: 'word-counter', name: 'Word Counter', cat: 'text', icon: 'fa-font', desc: 'Count words, chars & paragraphs.' },
            { id: 'case-conv', name: 'Case Converter', cat: 'text', icon: 'fa-text-height', desc: 'UPPER, lower, Sentence case.' },
            { id: 'duplicate-remover', name: 'Remove Duplicates', cat: 'text', icon: 'fa-clone', desc: 'Clean up repetitive lines.' },
            { id: 'text-cleaner', name: 'Text Cleaner', cat: 'text', icon: 'fa-broom', desc: 'Remove extra spaces & HTML.' },
            { id: 'text-reverse', name: 'Text Reverser', cat: 'text', icon: 'fa-backward', desc: 'Reverse your string content.' },
            { id: 'text-sorter', name: 'Text Sorter', cat: 'text', icon: 'fa-sort-alpha-down', desc: 'Alphabetical A-Z or Z-A sorting.' },
            { id: 'find-replace', name: 'Find & Replace', cat: 'text', icon: 'fa-search-plus', desc: 'Quickly swap text segments.' },
            
            // CALCULATORS
            { id: 'age-calc', name: 'Age Calculator', cat: 'calc', icon: 'fa-calendar-alt', desc: 'Calculate exact age in days.' },
            { id: 'bmi-calc', name: 'BMI Calculator', cat: 'calc', icon: 'fa-weight', desc: 'Body Mass Index calculator.' },
            { id: 'pct-calc', name: 'Percentage Calc', cat: 'calc', icon: 'fa-percent', desc: 'Simple percentage math tools.' },
            { id: 'emi-calc', name: 'EMI Calculator', cat: 'calc', icon: 'fa-money-bill-wave', desc: 'Calculate loan installments.' },
            { id: 'unit-conv', name: 'Unit Converter', cat: 'calc', icon: 'fa-exchange-alt', desc: 'Distance, Mass, Temp units.' },

            // DEV TOOLS
            { id: 'json-fmt', name: 'JSON Formatter', cat: 'dev', icon: 'fa-code', desc: 'Prettify or Minify JSON data.' },
            { id: 'b64-enc', name: 'Base64 Encoder', cat: 'dev', icon: 'fa-link', desc: 'Encode or Decode Base64.' },
            { id: 'pwd-gen', name: 'Password Gen', cat: 'dev', icon: 'fa-shield-alt', desc: 'Secure random passwords.' },
            { id: 'qr-gen', name: 'QR Generator', cat: 'dev', icon: 'fa-qrcode', desc: 'Generate custom QR codes.' },
            { id: 'html-fmt', name: 'HTML Formatter', cat: 'dev', icon: 'fa-file-code', desc: 'Clean and format HTML blocks.' },

            // IMAGE
            { id: 'img-preview', name: 'Image Preview', cat: 'img', icon: 'fa-eye', desc: 'View image metadata & size.' },
            { id: 'img-filter', name: 'Image Filters', cat: 'img', icon: 'fa-magic', desc: 'Grayscale, Sepia, Invert.' },

            // SEO
            { id: 'meta-gen', name: 'Meta Tag Gen', cat: 'seo', icon: 'fa-tags', desc: 'Generate SEO Meta tags.' },
            { id: 'robots-gen', name: 'Robots.txt Gen', cat: 'seo', icon: 'fa-robot', desc: 'Simple robots.txt file maker.' },

            // AI (Mock interfaces)
            { id: 'ai-writer', name: 'AI Text Writer', cat: 'ai', icon: 'fa-brain', desc: 'Interface for AI generation.' },
            { id: 'ai-summary', name: 'AI Summarizer', cat: 'ai', icon: 'fa-compress-alt', desc: 'Shorten long articles.' }
        ];

        /**
         * CORE LOGIC & ROUTING
         */
        function init() {
            renderCategories();
            renderTools(tools);
            updateTheme();
            renderTrending();
            renderHistory();
            
            // Hide loader
            setTimeout(() => {
                document.getElementById('page-loader').style.opacity = '0';
                setTimeout(() => document.getElementById('page-loader').style.display = 'none', 500);
            }, 1000);

            // Populate Admin Log
            const log = document.getElementById('activity-log');
            for(let i=0; i<5; i++) {
                log.innerHTML += `
                    <div class="flex items-center justify-between text-sm border-b dark:border-gray-700 pb-2">
                        <span>New user signed up from USA</span>
                        <span class="text-gray-400">${i+1}m ago</span>
                    </div>
                `;
            }
        }

        function navigateTo(section) {
            document.getElementById('home-section').classList.add('hidden-section');
            document.getElementById('tool-section').classList.add('hidden-section');
            document.getElementById('login-section').classList.add('hidden-section');
            document.getElementById('admin-section').classList.add('hidden-section');

            document.getElementById(`${section}-section`).classList.remove('hidden-section');
            window.scrollTo(0, 0);
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        function showToast(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg;
            t.classList.remove('opacity-0', 'translate-y-20');
            setTimeout(() => t.classList.add('opacity-0', 'translate-y-20'), 3000);
        }

        /**
         * THEME SWITCHER
         */
        const themeBtn = document.getElementById('theme-toggle');
        const mobileThemeBtn = document.getElementById('mobile-theme-toggle');

        function updateTheme() {
            if (state.theme === 'dark') {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
            localStorage.setItem('mfai_theme', state.theme);
        }

        themeBtn.onclick = () => {
            state.theme = state.theme === 'light' ? 'dark' : 'light';
            updateTheme();
        };

        /**
         * RENDER FUNCTIONS
         */
        function renderCategories() {
            const container = document.getElementById('category-filters');
            container.innerHTML = categories.map(c => `
                <button onclick="filterByCategory('${c.id}')" class="px-4 py-2 rounded-full border dark:border-gray-700 hover:bg-primary hover:text-white transition whitespace-nowrap text-sm font-medium">
                    <i class="fas ${c.icon} mr-2"></i>${c.name}
                </button>
            `).join('');
        }

        function renderTools(list) {
           
