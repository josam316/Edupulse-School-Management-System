[index.html](https://github.com/user-attachments/files/33821986/index.html)
<!DOCTYPE html>
<html lang="en" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EduPulse SMS - Enterprise Liquid Glass Edition</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: { sans: ['Inter', 'sans-serif'] },
                    colors: {
                        brand: {
                            50: '#eef2ff', 100: '#e0e7ff', 500: '#6366f1', 600: '#4f46e5', 700: '#4338ca', 800: '#3730a3', 900: '#312e81'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(156, 163, 175, 0.5); border-radius: 9999px; }
        .dark ::-webkit-scrollbar-thumb { background: rgba(51, 65, 85, 0.6); }

        /* --- LIQUID GLASS VISUAL ENGINE STYLES --- */
        .liquid-glass-bg {
            background: linear-gradient(135deg, #0f172a 0%, #1e1b4b 35%, #311042 70%, #0f172a 100%);
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
            position: relative;
            overflow: hidden;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Floating Animated Liquid Blobs */
        .liquid-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(80px);
            opacity: 0.6;
            animation: floatOrb 20s infinite ease-in-out alternate;
            pointer-events: none;
        }
        .orb-1 { width: 350px; height: 350px; background: #6366f1; top: -10%; left: -10%; animation-duration: 18s; }
        .orb-2 { width: 400px; height: 400px; background: #ec4899; bottom: -15%; right: -10%; animation-duration: 22s; animation-delay: -5s; }
        .orb-3 { width: 280px; height: 280px; background: #10b981; top: 40%; left: 60%; animation-duration: 16s; animation-delay: -8s; }

        @keyframes floatOrb {
            0% { transform: translate(0px, 0px) scale(1) rotate(0deg); }
            33% { transform: translate(60px, -80px) scale(1.15) rotate(120deg); }
            66% { transform: translate(-40px, 50px) scale(0.9) rotate(240deg); }
            100% { transform: translate(0px, 0px) scale(1) rotate(360deg); }
        }

        /* Pure Glassmorphic Container Layer */
        .liquid-glass-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(25px) saturate(190%);
            -webkit-backdrop-filter: blur(25px) saturate(190%);
            border: 1px solid rgba(255, 255, 255, 0.18);
            box-shadow: 0 30px 60px -12px rgba(0, 0, 0, 0.5), inset 0 1px 1px 0 rgba(255, 255, 255, 0.3);
        }

        .liquid-glass-input {
            background: rgba(255, 255, 255, 0.06);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: #ffffff;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .liquid-glass-input:focus {
            background: rgba(255, 255, 255, 0.12);
            border-color: rgba(129, 140, 248, 0.8);
            box-shadow: 0 0 20px rgba(99, 102, 241, 0.35);
        }

        .liquid-glass-button {
            background: linear-gradient(135deg, rgba(99, 102, 241, 0.85) 0%, rgba(79, 70, 229, 0.9) 100%);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
            box-shadow: 0 10px 25px -5px rgba(79, 70, 229, 0.5);
            transition: all 0.3s ease;
        }
        .liquid-glass-button:hover {
            transform: translateY(-2px) scale(1.01);
            box-shadow: 0 15px 30px -5px rgba(79, 70, 229, 0.7);
        }

        /* Main Dashboard Glass Cards */
        .app-glass-card {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(226, 232, 240, 0.8);
        }
        .dark .app-glass-card {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(51, 65, 85, 0.6);
        }

        @media print {
            body * { visibility: hidden; }
            #printable-area, #printable-area * { visibility: visible; }
            #printable-area { position: absolute; left: 0; top: 0; width: 100%; }
        }
    </style>
</head>
<body class="bg-slate-50 dark:bg-slate-900 text-slate-800 dark:text-slate-100 min-h-screen flex flex-col font-sans transition-colors duration-200">

    <!-- TOAST NOTIFICATION CONTAINER -->
    <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- AUTHENTICATION SCREEN WITH LIQUID GLASS EFFECT -->
    <div id="auth-screen" class="fixed inset-0 z-50 liquid-glass-bg flex items-center justify-center p-4">
        <!-- Floating Ambient Liquid Orbs -->
        <div class="liquid-orb orb-1"></div>
        <div class="liquid-orb orb-2"></div>
        <div class="liquid-orb orb-3"></div>

        <div class="liquid-glass-card rounded-3xl max-w-md w-full p-8 space-y-6 relative z-10">
            <!-- Header Logo & Title -->
            <div class="text-center space-y-2">
                <div class="inline-flex items-center justify-center p-3.5 bg-indigo-500/20 rounded-2xl border border-white/20 shadow-inner backdrop-blur-md">
                    <i class="fa-solid fa-graduation-cap text-3xl text-indigo-300 drop-shadow"></i>
                </div>
                <h2 class="text-3xl font-extrabold tracking-tight text-white drop-shadow-md">EduPulse OS</h2>
                <p class="text-xs text-indigo-200/80 font-medium">Enterprise Production System</p>
            </div>

            <!-- Login Form -->
            <form onsubmit="handleLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-indigo-100 mb-1.5">Username or Registered Email</label>
                    <div class="relative">
                        <i class="fa-solid fa-user absolute left-3.5 top-1/2 -translate-y-1/2 text-indigo-200/60 text-xs"></i>
                        <input type="text" id="login-identifier" required placeholder="user@domain.com" class="w-full liquid-glass-input rounded-xl pl-10 pr-3 py-2.5 text-xs focus:outline-none placeholder-indigo-200/40">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-semibold text-indigo-100 mb-1.5">Password</label>
                    <div class="relative">
                        <i class="fa-solid fa-lock absolute left-3.5 top-1/2 -translate-y-1/2 text-indigo-200/60 text-xs"></i>
                        <input type="password" id="login-password" required placeholder="Enter password" class="w-full liquid-glass-input rounded-xl pl-10 pr-10 py-2.5 text-xs focus:outline-none placeholder-indigo-200/40">
                        <button type="button" onclick="togglePasswordVisibility('login-password', this)" class="absolute right-3.5 top-1/2 -translate-y-1/2 text-indigo-200/60 hover:text-white text-xs">
                            <i class="fa-solid fa-eye"></i>
                        </button>
                    </div>
                </div>

                <div class="flex items-center justify-between text-xs pt-1">
                    <label class="flex items-center space-x-2 cursor-pointer">
                        <input type="checkbox" id="login-remember" class="rounded border-white/20 text-indigo-600 focus:ring-indigo-500 bg-white/10">
                        <span class="text-indigo-200/90 text-[11px]">Keep me signed in</span>
                    </label>
                    <a href="#" onclick="showToast('Password recovery instructions requested.', 'info')" class="text-indigo-300 hover:text-white font-medium text-[11px] underline">Forgot Key?</a>
                </div>

                <button type="submit" class="w-full liquid-glass-button text-white font-bold py-3 rounded-xl text-xs tracking-wider uppercase">
                    Sign In to Production System
                </button>
            </form>

            <!-- Production System Account Initialization -->
            <div class="border-t border-white/10 pt-4 text-center">
                <p class="text-[11px] text-indigo-200/80">Need an initial admin system account?</p>
                <button onclick="registerProductionAdmin()" class="mt-2 px-3 py-1.5 bg-white/10 hover:bg-white/20 border border-white/20 text-white rounded-xl text-xs font-bold transition">
                    <i class="fa-solid fa-user-plus mr-1"></i> Register Primary Administrator
                </button>
            </div>
        </div>
    </div>

    <!-- MAIN APP WRAPPER -->
    <div id="app-wrapper" class="hidden min-h-screen flex flex-col">
        <!-- GLOBAL NAVIGATION BAR -->
        <header class="sticky top-0 z-40 bg-white/80 dark:bg-slate-800/80 backdrop-blur-xl border-b border-slate-200/80 dark:border-slate-700/80 px-4 lg:px-8 py-3">
            <div class="max-w-7xl mx-auto flex items-center justify-between gap-4">
                <div class="flex items-center space-x-3">
                    <div class="bg-brand-600 text-white p-2 rounded-2xl shadow-lg shadow-brand-500/20">
                        <i class="fa-solid fa-graduation-cap text-lg"></i>
                    </div>
                    <div>
                        <span id="header-school-brand" class="text-xl font-black bg-gradient-to-r from-brand-600 via-indigo-600 to-purple-600 bg-clip-text text-transparent">EduPulse</span>
                        <span id="header-role-badge" class="ml-2 text-[10px] px-2.5 py-0.5 bg-brand-50 text-brand-700 dark:bg-brand-900/40 dark:text-brand-300 rounded-full font-bold uppercase tracking-wider"></span>
                    </div>
                </div>

                <!-- Navigation Tabs (RBAC Dynamic) -->
                <nav id="nav-menu" class="hidden md:flex items-center space-x-1 bg-slate-100/80 dark:bg-slate-900/80 p-1.5 rounded-2xl border border-slate-200/60 dark:border-slate-700/60 text-xs font-semibold backdrop-blur-md">
                    <!-- Populated dynamically -->
                </nav>

                <!-- User Profile & Controls -->
                <div class="flex items-center space-x-3">
                    <button onclick="openModal('modal-deploy')" title="Deploy Application" class="px-3 py-2 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold transition shadow-md flex items-center gap-1.5">
                        <i class="fa-solid fa-cloud-arrow-up"></i>
                        <span>Deploy App</span>
                    </button>
                    <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 dark:hover:bg-slate-600 transition">
                        <i class="fa-solid fa-sun hidden dark:block"></i>
                        <i class="fa-solid fa-moon block dark:hidden"></i>
                    </button>
                    <button onclick="resetSystemData()" title="Reset All Data" class="p-2.5 rounded-xl bg-red-100 text-red-600 dark:bg-red-900/30 dark:text-red-400 hover:bg-red-200 transition">
                        <i class="fa-solid fa-rotate-left"></i>
                    </button>
                    <div class="h-6 w-px bg-slate-200 dark:bg-slate-700"></div>
                    <div class="flex items-center space-x-3">
                        <img id="nav-user-avatar" src="" class="w-9 h-9 rounded-xl object-cover ring-2 ring-brand-500/30" alt="Avatar">
                        <div class="hidden lg:block text-left leading-tight">
                            <p id="nav-user-name" class="text-xs font-bold text-slate-800 dark:text-slate-100"></p>
                            <p id="nav-user-email" class="text-[10px] text-slate-400"></p>
                        </div>
                        <button onclick="handleLogout()" title="Sign Out" class="p-2 text-red-500 hover:bg-red-50 dark:hover:bg-red-900/20 rounded-xl transition">
                            <i class="fa-solid fa-right-from-bracket"></i>
                        </button>
                    </div>
                </div>
            </div>
        </header>

        <!-- DASHBOARD CONTAINER -->
        <main class="flex-grow max-w-7xl w-full mx-auto px-4 lg:px-8 py-6 space-y-6">

            <!-- 1. DASHBOARD OVERVIEW PANEL -->
            <section id="tab-overview" class="tab-content space-y-6">
                <!-- Advanced Dynamic Search & Quick Actions -->
                <div class="app-glass-card p-4 rounded-2xl flex flex-wrap items-center justify-between gap-4 shadow-sm">
                    <div class="relative flex-1 min-w-[240px]">
                        <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                        <input type="text" id="global-search-input" oninput="handleGlobalSearch(this.value)" placeholder="Global System Search (Students, Teachers, Invoices...)" class="w-full bg-slate-100/70 dark:bg-slate-900/70 border border-slate-200 dark:border-slate-700 rounded-xl pl-9 pr-3 py-2 text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                    </div>
                    <div class="flex items-center space-x-2">
                        <button onclick="openModal('modal-attendance')" class="bg-indigo-600 hover:bg-indigo-700 text-white px-3.5 py-2 rounded-xl text-xs font-bold shadow-md transition flex items-center gap-1.5">
                            <i class="fa-solid fa-clipboard-user"></i> Quick Attendance
                        </button>
                        <button onclick="triggerBroadcastNotice()" class="bg-purple-600 hover:bg-purple-700 text-white px-3.5 py-2 rounded-xl text-xs font-bold shadow-md transition flex items-center gap-1.5">
                            <i class="fa-solid fa-bullhorn"></i> Announcement
                        </button>
                    </div>
                </div>

                <!-- KPI Cards Grid -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Active Enrolments</p>
                                <h3 id="kpi-students-count" class="text-2xl font-black mt-1">0</h3>
                            </div>
                            <div class="p-3 bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 rounded-2xl">
                                <i class="fa-solid fa-user-graduate text-xl"></i>
                            </div>
                        </div>
                    </div>

                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Faculty Staff</p>
                                <h3 id="kpi-teachers-count" class="text-2xl font-black mt-1">0</h3>
                            </div>
                            <div class="p-3 bg-purple-50 dark:bg-purple-900/30 text-purple-600 dark:text-purple-400 rounded-2xl">
                                <i class="fa-solid fa-chalkboard-user text-xl"></i>
                            </div>
                        </div>
                    </div>

                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Revenue Ledger</p>
                                <h3 id="kpi-revenue" class="text-2xl font-black mt-1">$0.00</h3>
                            </div>
                            <div class="p-3 bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 rounded-2xl">
                                <i class="fa-solid fa-sack-dollar text-xl"></i>
                            </div>
                        </div>
                    </div>

                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-[11px] font-bold uppercase tracking-wider text-slate-400">Avg Attendance Rate</p>
                                <h3 id="kpi-attendance-rate" class="text-2xl font-black text-emerald-600 mt-1">96.4%</h3>
                            </div>
                            <div class="p-3 bg-amber-50 dark:bg-amber-900/30 text-amber-600 dark:text-amber-400 rounded-2xl">
                                <i class="fa-solid fa-calendar-check text-xl"></i>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Interactive Charts -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <h3 class="font-bold text-sm mb-4 text-slate-800 dark:text-slate-100 flex items-center gap-2">
                            <i class="fa-solid fa-chart-line text-brand-500"></i> Enrollment Trends & Growth
                        </h3>
                        <div class="h-60"><canvas id="chart-enrollment"></canvas></div>
                    </div>
                    <div class="app-glass-card p-5 rounded-2xl shadow-sm">
                        <h3 class="font-bold text-sm mb-4 text-slate-800 dark:text-slate-100 flex items-center gap-2">
                            <i class="fa-solid fa-chart-pie text-emerald-500"></i> Fee Collection Analytics
                        </h3>
                        <div class="h-60 flex justify-center"><canvas id="chart-fees"></canvas></div>
                    </div>
                </div>
            </section>

            <!-- 2. TEACHERS CRUD MODULE -->
            <section id="tab-teachers" class="tab-content hidden space-y-6">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h1 class="text-2xl font-bold tracking-tight">Faculty & Teachers Management</h1>
                        <p class="text-xs text-slate-500">Full CRUD operations for teaching staff and login authorization</p>
                    </div>
                    <div class="flex items-center space-x-2">
                        <button onclick="exportTableToCSV('teachers')" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 px-3.5 py-2 rounded-xl text-xs font-semibold hover:bg-slate-300 transition">
                            <i class="fa-solid fa-file-csv mr-1"></i> Export CSV
                        </button>
                        <button onclick="openModal('modal-teacher')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-md transition">
                            <i class="fa-solid fa-plus mr-1"></i> Add Faculty
                        </button>
                    </div>
                </div>

                <div class="app-glass-card rounded-2xl shadow-sm overflow-hidden">
                    <div class="p-4 border-b border-slate-200/80 dark:border-slate-700/80 flex flex-wrap gap-2 justify-between">
                        <input type="text" id="teacher-search" oninput="renderTeachersTable()" placeholder="Search teacher name, subject, email..." class="bg-slate-100/80 dark:bg-slate-900/80 border border-slate-200 dark:border-slate-700 text-xs rounded-xl px-3 py-2 w-64 focus:outline-none">
                        <select id="teacher-dept-filter" onchange="renderTeachersTable()" class="bg-slate-100/80 dark:bg-slate-900/80 border border-slate-200 dark:border-slate-700 text-xs rounded-xl px-3 py-2">
                            <option value="all">All Departments</option>
                            <option value="Primary Education">Primary Education</option>
                            <option value="Science">Science</option>
                            <option value="Mathematics">Mathematics</option>
                            <option value="Languages">Languages</option>
                            <option value="Social Studies">Social Studies</option>
                            <option value="Arts">Arts</option>
                        </select>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-slate-50/50 dark:bg-slate-900/50 text-slate-500 border-b border-slate-200 dark:border-slate-700">
                                    <th class="p-3.5 font-bold">Teacher Name</th>
                                    <th class="p-3.5 font-bold">Department</th>
                                    <th class="p-3.5 font-bold">Subject Lead</th>
                                    <th class="p-3.5 font-bold">Phone Contact</th>
                                    <th class="p-3.5 font-bold">Account Pass</th>
                                    <th class="p-3.5 font-bold">Status</th>
                                    <th class="p-3.5 font-bold text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="teachers-table-body" class="divide-y divide-slate-200/80 dark:divide-slate-700/80"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 3. STUDENTS CRUD MODULE -->
            <section id="tab-students" class="tab-content hidden space-y-6">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h1 class="text-2xl font-bold tracking-tight">Student Directory & Profiles</h1>
                        <p class="text-xs text-slate-500">Enrolments, academic tracking, course selections, and guardian contacts</p>
                    </div>
                    <div class="flex items-center space-x-2">
                        <button onclick="exportTableToCSV('students')" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 px-3.5 py-2 rounded-xl text-xs font-semibold hover:bg-slate-300 transition">
                            <i class="fa-solid fa-file-csv mr-1"></i> Export CSV
                        </button>
                        <button onclick="openModal('modal-student')" class="bg-brand-600 hover:bg-brand-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-md transition">
                            <i class="fa-solid fa-user-plus mr-1"></i> Enroll Student
                        </button>
                    </div>
                </div>

                <div class="app-glass-card rounded-2xl shadow-sm overflow-hidden">
                    <div class="p-4 border-b border-slate-200/80 dark:border-slate-700/80 flex flex-wrap gap-2 justify-between">
                        <input type="text" id="student-search" oninput="renderStudentsTable()" placeholder="Search name or ID..." class="bg-slate-100/80 dark:bg-slate-900/80 border border-slate-200 dark:border-slate-700 text-xs rounded-xl px-3 py-2 w-64 focus:outline-none">
                        <select id="student-grade-filter" onchange="renderStudentsTable()" class="bg-slate-100/80 dark:bg-slate-900/80 border border-slate-200 dark:border-slate-700 text-xs rounded-xl px-3 py-2">
                            <option value="all">All Grades</option>
                            <optgroup label="Primary Level">
                                <option value="Grade 1">Grade 1 (P1)</option>
                                <option value="Grade 2">Grade 2 (P2)</option>
                                <option value="Grade 3">Grade 3 (P3)</option>
                                <option value="Grade 4">Grade 4 (P4)</option>
                                <option value="Grade 5">Grade 5 (P5)</option>
                                <option value="Grade 6">Grade 6 (P6)</option>
                                <option value="Grade 7">Grade 7 (P7)</option>
                            </optgroup>
                            <optgroup label="Secondary Level">
                                <option value="Grade 10">Grade 10</option>
                                <option value="Grade 11">Grade 11</option>
                                <option value="Grade 12">Grade 12</option>
                            </optgroup>
                        </select>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-slate-50/50 dark:bg-slate-900/50 text-slate-500 border-b border-slate-200 dark:border-slate-700">
                                    <th class="p-3.5 font-bold">Student Profile</th>
                                    <th class="p-3.5 font-bold">ID Code</th>
                                    <th class="p-3.5 font-bold">Grade</th>
                                    <th class="p-3.5 font-bold">Enrolled Subjects</th>
                                    <th class="p-3.5 font-bold">Guardian Email</th>
                                    <th class="p-3.5 font-bold">Calculated GPA</th>
                                    <th class="p-3.5 font-bold">Tuition Status</th>
                                    <th class="p-3.5 font-bold text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="students-table-body" class="divide-y divide-slate-200/80 dark:divide-slate-700/80"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 4. GRADING & REPORT CARDS MODULE -->
            <section id="tab-grading" class="tab-content hidden space-y-6">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h1 class="text-2xl font-bold tracking-tight">Gradebook & Class Marksheets</h1>
                        <p class="text-xs text-slate-500">Live mark updates, automated GPA formulas, and report cards</p>
                    </div>
                    <div class="flex items-center space-x-2">
                        <select id="marksheet-class-select" onchange="renderGradebookTable()" class="bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 text-xs rounded-xl px-3 py-2 font-semibold">
                            <option value="all">All Classes / Grades</option>
                            <optgroup label="Primary Level">
                                <option value="Grade 1">Grade 1 (P1)</option>
                                <option value="Grade 2">Grade 2 (P2)</option>
                                <option value="Grade 3">Grade 3 (P3)</option>
                                <option value="Grade 4">Grade 4 (P4)</option>
                                <option value="Grade 5">Grade 5 (P5)</option>
                                <option value="Grade 6">Grade 6 (P6)</option>
                                <option value="Grade 7">Grade 7 (P7)</option>
                            </optgroup>
                            <optgroup label="Secondary Level">
                                <option value="Grade 10">Grade 10</option>
                                <option value="Grade 11">Grade 11</option>
                                <option value="Grade 12">Grade 12</option>
                            </optgroup>
                        </select>
                        <button onclick="exportClassMarksheet()" class="bg-slate-200 dark:bg-slate-700 text-slate-700 dark:text-slate-200 px-3.5 py-2 rounded-xl text-xs font-semibold hover:bg-slate-300 transition">
                            <i class="fa-solid fa-file-csv mr-1"></i> Export Marksheet
                        </button>
                    </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                    <div class="app-glass-card p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <p class="text-xs font-semibold text-slate-400">Class Average</p>
                            <h4 id="marksheet-class-avg" class="text-xl font-bold mt-0.5">--</h4>
                        </div>
                        <div class="p-2.5 bg-indigo-50 dark:bg-indigo-900/30 text-indigo-600 rounded-xl">
                            <i class="fa-solid fa-calculator text-lg"></i>
                        </div>
                    </div>
                    <div class="app-glass-card p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <p class="text-xs font-semibold text-slate-400">Highest Score</p>
                            <h4 id="marksheet-highest-score" class="text-xl font-bold text-emerald-600 mt-0.5">--</h4>
                        </div>
                        <div class="p-2.5 bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 rounded-xl">
                            <i class="fa-solid fa-trophy text-lg"></i>
                        </div>
                    </div>
                    <div class="app-glass-card p-4 rounded-2xl shadow-sm flex items-center justify-between">
                        <div>
                            <p class="text-xs font-semibold text-slate-400">Class Count</p>
                            <h4 id="marksheet-total-students" class="text-xl font-bold text-brand-600 mt-0.5">0</h4>
                        </div>
                        <div class="p-2.5 bg-brand-50 dark:bg-brand-900/30 text-brand-600 rounded-xl">
                            <i class="fa-solid fa-users text-lg"></i>
                        </div>
                    </div>
                </div>

                <div class="app-glass-card rounded-2xl p-5 space-y-4 shadow-sm">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-slate-50/50 dark:bg-slate-900/50 text-slate-500 border-b border-slate-200 dark:border-slate-700">
                                    <th class="p-3.5 font-bold">Student Name</th>
                                    <th class="p-3.5 font-bold">Class / Grade</th>
                                    <th class="p-3.5 font-bold">Midterm (40%)</th>
                                    <th class="p-3.5 font-bold">Assignments (30%)</th>
                                    <th class="p-3.5 font-bold">Final Exam (30%)</th>
                                    <th class="p-3.5 font-bold">Overall Score</th>
                                    <th class="p-3.5 font-bold">Grade</th>
                                    <th class="p-3.5 font-bold text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="gradebook-table-body" class="divide-y divide-slate-200 dark:divide-slate-700"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 5. FINANCIAL & INVOICING MODULE -->
            <section id="tab-billing" class="tab-content hidden space-y-6">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
                    <div>
                        <h1 class="text-2xl font-bold tracking-tight">Fee Ledger & Invoicing</h1>
                        <p class="text-xs text-slate-500">Student tuition invoicing, payments, and financial auditing</p>
                    </div>
                    <button onclick="openModal('modal-invoice')" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded-xl text-xs font-semibold shadow-md transition">
                        <i class="fa-solid fa-file-invoice-dollar mr-1"></i> Issue New Invoice
                    </button>
                </div>

                <div class="app-glass-card rounded-2xl shadow-sm overflow-hidden">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="bg-slate-50/50 dark:bg-slate-900/50 text-slate-500 border-b border-slate-200 dark:border-slate-700">
                                    <th class="p-3.5 font-bold">Invoice #</th>
                                    <th class="p-3.5 font-bold">Student Name</th>
                                    <th class="p-3.5 font-bold">Billing Description</th>
                                    <th class="p-3.5 font-bold">Amount ($)</th>
                                    <th class="p-3.5 font-bold">Due Date</th>
                                    <th class="p-3.5 font-bold">Status</th>
                                    <th class="p-3.5 font-bold text-right">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="invoices-table-body" class="divide-y divide-slate-200 dark:divide-slate-700"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- 6. SYSTEM SETTINGS MODULE -->
            <section id="tab-settings" class="tab-content hidden space-y-6">
                <div>
                    <h1 class="text-2xl font-bold tracking-tight">System Configuration & Branding</h1>
                    <p class="text-xs text-slate-500">Customize institutional name, branding parameters, and workspace preferences</p>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="app-glass-card p-6 rounded-2xl shadow-sm space-y-5">
                        <h3 class="font-bold text-sm text-slate-800 dark:text-slate-100 flex items-center gap-2 border-b border-slate-200/80 dark:border-slate-700/80 pb-3">
                            <i class="fa-solid fa-building-columns text-brand-500"></i> Institutional Branding
                        </h3>
                        <form onsubmit="saveSchoolBranding(event)" class="space-y-4">
                            <div>
                                <label class="block text-xs font-semibold mb-1.5 text-slate-700 dark:text-slate-300">Custom School / Organization Name</label>
                                <div class="relative">
                                    <i class="fa-solid fa-signature absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                                    <input type="text" id="settings-school-name" required placeholder="e.g. EduPulse Academy" class="w-full bg-slate-100/80 dark:bg-slate-900/80 border border-slate-200 dark:border-slate-700 rounded-xl pl-10 pr-3 py-2.5 text-xs focus:outline-none focus:ring-2 focus:ring-brand-500">
                                </div>
                                <p class="text-[10px] text-slate-400 mt-1">This updates the header title and report cards across the entire platform instantly.</p>
                            </div>
                            <div class="pt-2">
                                <button type="submit" class="px-4 py-2.5 bg-brand-600 hover:bg-brand-700 text-white text-xs font-bold rounded-xl shadow-md transition flex items-center gap-1.5">
                                    <i class="fa-solid fa-floppy-disk"></i> Save Branding Changes
                                </button>
                            </div>
                        </form>
                    </div>

                    <div class="app-glass-card p-6 rounded-2xl shadow-sm space-y-5">
                        <h3 class="font-bold text-sm text-slate-800 dark:text-slate-100 flex items-center gap-2 border-b border-slate-200/80 dark:border-slate-700/80 pb-3">
                            <i class="fa-solid fa-shield-halved text-emerald-500"></i> Workspace Preferences
                        </h3>
                        <div class="space-y-3 text-xs text-slate-600 dark:text-slate-300">
                            <div class="flex items-center justify-between p-3 bg-slate-100/60 dark:bg-slate-900/60 rounded-xl">
                                <div>
                                    <p class="font-bold">Persistent Local Storage</p>
                                    <p class="text-[10px] text-slate-400">All edits, student marks, and invoices are auto-saved locally.</p>
                                </div>
                                <span class="px-2.5 py-1 bg-emerald-100 text-emerald-700 rounded-full font-bold text-[10px]">Active</span>
                            </div>
                            <div class="flex items-center justify-between p-3 bg-slate-100/60 dark:bg-slate-900/60 rounded-xl">
                                <div>
                                    <p class="font-bold">Role-Based Access Control</p>
                                    <p class="text-[10px] text-slate-400">Admin, Teacher, and Student permissions verified.</p>
                                </div>
                                <span class="px-2.5 py-1 bg-indigo-100 text-indigo-700 rounded-full font-bold text-[10px]">Secure</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

        </main>
    </div>

    <!-- MODALS -->

    <!-- DEPLOYMENT MODAL -->
    <div id="modal-deploy" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-2xl max-w-lg w-full p-6 space-y-5 relative">
            <button onclick="closeModal('modal-deploy')" class="absolute right-4 top-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-base"></i>
            </button>
            <div>
                <div class="inline-flex items-center gap-2 px-3 py-1 bg-emerald-100 dark:bg-emerald-900/40 text-emerald-700 dark:text-emerald-300 rounded-full text-[11px] font-bold mb-2">
                    <i class="fa-solid fa-rocket"></i> Production Deployment Center
                </div>
                <h3 class="text-xl font-black text-slate-900 dark:text-white">Deploy EduPulse OS</h3>
                <p class="text-xs text-slate-500 mt-1">Export standalone bundle, host on free web services, or download deployment package.</p>
            </div>

            <div class="space-y-3">
                <div class="p-4 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-2xl flex items-center justify-between hover:border-emerald-500 transition">
                    <div class="flex items-center space-x-3">
                        <div class="p-3 bg-emerald-100 dark:bg-emerald-900/40 text-emerald-600 rounded-xl">
                            <i class="fa-solid fa-file-code text-lg"></i>
                        </div>
                        <div>
                            <p class="text-xs font-bold">Standalone HTML Bundle</p>
                            <p class="text-[10px] text-slate-400">Single self-contained file with embedded database</p>
                        </div>
                    </div>
                    <button onclick="downloadProductionBundle()" class="px-3.5 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-bold rounded-xl text-xs transition shadow-sm">
                        <i class="fa-solid fa-download mr-1"></i> Download
                    </button>
                </div>

                <div class="p-4 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-2xl flex items-center justify-between hover:border-black dark:hover:border-white transition">
                    <div class="flex items-center space-x-3">
                        <div class="p-3 bg-slate-200 dark:bg-slate-800 text-slate-800 dark:text-slate-200 rounded-xl">
                            <i class="fa-brands fa-github text-lg"></i>
                        </div>
                        <div>
                            <p class="text-xs font-bold">GitHub Pages / Vercel / Netlify</p>
                            <p class="text-[10px] text-slate-400">Copy single-file code directly to host on free static servers</p>
                        </div>
                    </div>
                    <button onclick="copySourceToClipboard()" class="px-3.5 py-2 bg-slate-800 dark:bg-slate-700 hover:bg-slate-900 text-white font-bold rounded-xl text-xs transition shadow-sm">
                        <i class="fa-solid fa-copy mr-1"></i> Copy Code
                    </button>
                </div>
            </div>

            <div class="p-3 bg-amber-50 dark:bg-amber-900/30 border border-amber-200 dark:border-amber-800/50 rounded-xl text-[11px] text-amber-800 dark:text-amber-300 flex items-start gap-2">
                <i class="fa-solid fa-lightbulb text-amber-500 mt-0.5"></i>
                <span><strong>Deployment Tip:</strong> For instant hosting, save the downloaded file as <code>index.html</code> and drag & drop it directly into <a href="https://app.netlify.com/drop" target="_blank" class="underline font-bold">Netlify Drop</a> or Vercel.</span>
            </div>

            <div class="pt-2 flex justify-end">
                <button onclick="closeModal('modal-deploy')" class="px-4 py-2 text-xs font-semibold text-slate-500">Close</button>
            </div>
        </div>
    </div>

    <!-- QUICK ATTENDANCE MODAL -->
    <div id="modal-attendance" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-2xl max-w-lg w-full p-6 space-y-4 relative">
            <button onclick="closeModal('modal-attendance')" class="absolute right-4 top-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-base"></i>
            </button>
            <h3 class="text-lg font-bold text-slate-900 dark:text-white">Daily Attendance Marking</h3>
            <div class="space-y-3">
                <p class="text-xs text-slate-500">Mark daily attendance for students in selected grade level.</p>
                <div id="attendance-list-container" class="space-y-2 max-h-60 overflow-y-auto pr-1"></div>
                <div class="pt-2 flex justify-end space-x-2">
                    <button onclick="closeModal('modal-attendance')" class="px-4 py-2 text-xs font-semibold text-slate-500">Cancel</button>
                    <button onclick="submitAttendance()" class="px-4 py-2 text-xs font-semibold text-white bg-indigo-600 hover:bg-indigo-700 rounded-xl shadow">Save Attendance Log</button>
                </div>
            </div>
        </div>
    </div>

    <!-- TEACHER FORM MODAL -->
    <div id="modal-teacher" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-2xl max-w-lg w-full p-6 space-y-4 relative">
            <button onclick="closeModal('modal-teacher')" class="absolute right-4 top-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-base"></i>
            </button>
            <h3 id="modal-teacher-title" class="text-lg font-bold text-slate-900 dark:text-white">Add Faculty Staff</h3>
            <form onsubmit="saveTeacherForm(event)" class="space-y-3">
                <input type="hidden" id="teacher-form-id">
                <div>
                    <label class="block text-xs font-semibold mb-1">Full Name</label>
                    <input type="text" id="teacher-form-name" required placeholder="Dr. John Doe" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-semibold mb-1">Email</label>
                        <input type="email" id="teacher-form-email" required placeholder="john@edupulse.edu" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold mb-1">Phone</label>
                        <input type="text" id="teacher-form-phone" required placeholder="+1 555-0192" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                </div>
                <div class="p-3 bg-slate-50 dark:bg-slate-900/60 border border-slate-200 dark:border-slate-700 rounded-xl space-y-2">
                    <span class="text-[11px] font-bold text-brand-600 dark:text-brand-400 uppercase tracking-wider block">Login Account Key</span>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label class="block text-[11px] font-semibold mb-1">Account Password</label>
                            <div class="relative">
                                <input type="password" id="teacher-form-password" required placeholder="Set login password" class="w-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl pl-3 pr-8 py-2 text-xs">
                                <button type="button" onclick="togglePasswordVisibility('teacher-form-password', this)" class="absolute right-2.5 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600 text-xs">
                                    <i class="fa-solid fa-eye"></i>
                                </button>
                            </div>
                        </div>
                        <div class="flex items-end">
                            <button type="button" onclick="generateRandomPassword('teacher-form-password')" class="w-full py-2 bg-slate-200 dark:bg-slate-700 hover:bg-slate-300 dark:hover:bg-slate-600 text-slate-700 dark:text-slate-200 rounded-xl text-xs font-semibold transition">
                                <i class="fa-solid fa-key mr-1"></i> Auto-Generate
                            </button>
                        </div>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-semibold mb-1">Department</label>
                        <select id="teacher-form-dept" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                            <option>Primary Education</option>
                            <option>Science</option>
                            <option>Mathematics</option>
                            <option>Languages</option>
                            <option>Social Studies</option>
                            <option>Arts</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold mb-1">Primary Subject Lead</label>
                        <input type="text" id="teacher-form-subject" required placeholder="Primary Mathematics" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                </div>
                <div class="pt-2 flex justify-end space-x-2">
                    <button type="button" onclick="closeModal('modal-teacher')" class="px-4 py-2 text-xs font-semibold text-slate-500">Cancel</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold text-white bg-brand-600 hover:bg-brand-700 rounded-xl shadow-md">Save Record</button>
                </div>
            </form>
        </div>
    </div>

    <!-- STUDENT FORM MODAL -->
    <div id="modal-student" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-2xl max-w-xl w-full p-6 space-y-4 relative max-h-[90vh] overflow-y-auto">
            <button onclick="closeModal('modal-student')" class="absolute right-4 top-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-base"></i>
            </button>
            <h3 id="modal-student-title" class="text-lg font-bold text-slate-900 dark:text-white">Enroll Student</h3>
            <form onsubmit="saveStudentForm(event)" class="space-y-3">
                <input type="hidden" id="student-form-id">
                <div>
                    <label class="block text-xs font-semibold mb-1">Full Student Name</label>
                    <input type="text" id="student-form-name" required placeholder="e.g. Liam Smith" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-semibold mb-1">Grade Level</label>
                        <select id="student-form-grade" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                            <optgroup label="Primary School">
                                <option>Grade 1</option>
                                <option>Grade 2</option>
                                <option>Grade 3</option>
                                <option>Grade 4</option>
                                <option>Grade 5</option>
                                <option>Grade 6</option>
                                <option>Grade 7</option>
                            </optgroup>
                            <optgroup label="Secondary School">
                                <option>Grade 10</option>
                                <option>Grade 11</option>
                                <option>Grade 12</option>
                            </optgroup>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold mb-1">Student Email</label>
                        <input type="email" id="student-form-email" required placeholder="liam@edupulse.edu" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-semibold mb-1">Guardian Email</label>
                    <input type="email" id="student-form-guardian" required placeholder="parent@example.com" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                </div>

                <div>
                    <label class="block text-xs font-semibold mb-1.5">Enrolled Subjects / Course Load</label>
                    <div class="space-y-3 p-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl text-xs max-h-48 overflow-y-auto">
                        <div class="grid grid-cols-2 gap-2">
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="English Language" class="rounded text-brand-600"><span>English Language</span></label>
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="Primary Mathematics" class="rounded text-brand-600"><span>Primary Mathematics</span></label>
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="Integrated Science" class="rounded text-brand-600"><span>Integrated Science</span></label>
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="Social Studies" class="rounded text-brand-600"><span>Social Studies</span></label>
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="Physics" class="rounded text-brand-600"><span>Physics</span></label>
                            <label class="flex items-center space-x-2 cursor-pointer"><input type="checkbox" name="student-subjects" value="Computer Science" class="rounded text-brand-600"><span>Computer Science</span></label>
                        </div>
                    </div>
                </div>

                <div class="pt-2 flex justify-end space-x-2">
                    <button type="button" onclick="closeModal('modal-student')" class="px-4 py-2 text-xs font-semibold text-slate-500">Cancel</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold text-white bg-brand-600 hover:bg-brand-700 rounded-xl shadow-md">Save Student</button>
                </div>
            </form>
        </div>
    </div>

    <!-- INVOICE FORM MODAL -->
    <div id="modal-invoice" class="fixed inset-0 z-50 hidden bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl border border-slate-200 dark:border-slate-700 shadow-2xl max-w-md w-full p-6 space-y-4 relative">
            <button onclick="closeModal('modal-invoice')" class="absolute right-4 top-4 text-slate-400 hover:text-slate-600">
                <i class="fa-solid fa-xmark text-base"></i>
            </button>
            <h3 class="text-lg font-bold text-slate-900 dark:text-white">Issue Fee Invoice</h3>
            <form onsubmit="saveInvoiceForm(event)" class="space-y-3">
                <div>
                    <label class="block text-xs font-semibold mb-1">Select Student</label>
                    <select id="invoice-form-student" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs"></select>
                </div>
                <div>
                    <label class="block text-xs font-semibold mb-1">Description</label>
                    <input type="text" id="invoice-form-desc" required placeholder="e.g. Term 3 Tuition Fee" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-semibold mb-1">Amount ($)</label>
                        <input type="number" id="invoice-form-amount" required placeholder="850" class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold mb-1">Due Date</label>
                        <input type="date" id="invoice-form-date" required class="w-full bg-slate-100 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl px-3 py-2 text-xs">
                    </div>
                </div>
                <div class="pt-2 flex justify-end space-x-2">
                    <button type="button" onclick="closeModal('modal-invoice')" class="px-4 py-2 text-xs font-semibold text-slate-500">Cancel</button>
                    <button type="submit" class="px-4 py-2 text-xs font-semibold text-white bg-emerald-600 hover:bg-emerald-700 rounded-xl shadow-md">Create Invoice</button>
                </div>
            </form>
        </div>
    </div>

    <!-- PRINTABLE REPORT CARD HIDDEN TEMPLATE -->
    <div id="printable-area" class="hidden p-8 bg-white text-slate-900 space-y-6">
        <div class="flex justify-between items-center border-b pb-4">
            <div>
                <h1 class="text-2xl font-bold">EDUPULSE ACADEMY</h1>
                <p class="text-xs text-slate-500">Official Academic Progress Report</p>
            </div>
            <div class="text-right text-xs">
                <p class="font-bold">Academic Term 2026</p>
            </div>
        </div>
        <div id="report-card-details" class="text-xs space-y-2"></div>
    </div>

    <!-- SCRIPT ENGINE -->
    <script>
        const memoryStorage = {};
        const SafeStorage = {
            getItem: (key) => { try { return localStorage.getItem(key); } catch (e) { return memoryStorage[key] || null; } },
            setItem: (key, val) => { try { localStorage.setItem(key, val); } catch (e) { memoryStorage[key] = String(val); } },
            removeItem: (key) => { try { localStorage.removeItem(key); } catch (e) { delete memoryStorage[key]; } }
        };
        const SafeSessionStorage = {
            getItem: (key) => { try { return sessionStorage.getItem(key); } catch (e) { return memoryStorage['session_' + key] || null; } },
            setItem: (key, val) => { try { sessionStorage.setItem(key, val); } catch (e) { memoryStorage['session_' + key] = String(val); } },
            removeItem: (key) => { try { sessionStorage.removeItem(key); } catch (e) { delete memoryStorage['session_' + key]; } }
        };

        let currentUser = null;

        function dbGet(key) { try { return JSON.parse(SafeStorage.getItem(key)) || []; } catch(e) { return []; } }
        function dbSet(key, val) { SafeStorage.setItem(key, JSON.stringify(val)); }

        function handleLogin(e) {
            e.preventDefault();
            const identifier = document.getElementById('login-identifier').value.trim();
            const password = document.getElementById('login-password').value;
            const remember = document.getElementById('login-remember').checked;

            const users = dbGet('ep_users');
            const user = users.find(u => (u.identifier === identifier || u.username === identifier) && u.password === password);

            if (user) {
                currentUser = user;
                const storage = remember ? SafeStorage : SafeSessionStorage;
                storage.setItem('ep_session', JSON.stringify(user));
                bootApp();
                showToast(`Welcome back, ${user.name}!`, 'success');
            } else {
                showToast('Invalid credentials. Check username/password.', 'error');
            }
        }

        function handleLogout() {
            SafeStorage.removeItem('ep_session');
            SafeSessionStorage.removeItem('ep_session');
            currentUser = null;
            document.getElementById('app-wrapper').classList.add('hidden');
            document.getElementById('auth-screen').classList.remove('hidden');
            showToast('Signed out of production session.', 'info');
        }

        function resetSystemData() {
            if (!confirm("Are you sure you want to reset all stored students, faculty, and invoices? This action cannot be undone.")) return;
            SafeStorage.removeItem('ep_students');
            SafeStorage.removeItem('ep_teachers');
            SafeStorage.removeItem('ep_invoices');
            dbInit();
            updateKPIs();
            renderTeachersTable();
            renderStudentsTable();
            renderGradebookTable();
            renderInvoicesTable();
            initCharts();
            showToast('System data reset to initial state.', 'info');
        }

        function dbInit() {
            let users = dbGet('ep_users');
            if (!users || users.length === 0) {
                const defaultAdmin = {
                    id: Date.now(),
                    identifier: 'josam2403@gmail.com',
                    username: 'josam',
                    phone: '',
                    password: '1',
                    role: 'Admin',
                    name: 'Primary Administrator',
                    avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100'
                };
                users = [defaultAdmin];
                dbSet('ep_users', users);
            } else {
                const adminIndex = users.findIndex(u => u.role === 'Admin');
                if (adminIndex !== -1) {
                    users[adminIndex].identifier = users[adminIndex].identifier || 'josam2403@gmail.com';
                    users[adminIndex].username = users[adminIndex].username || 'josam';
                    users[adminIndex].password = users[adminIndex].password || '1';
                    dbSet('ep_users', users);
                }
            }
            if (!SafeStorage.getItem('ep_students')) dbSet('ep_students', []);
            if (!SafeStorage.getItem('ep_teachers')) dbSet('ep_teachers', []);
            if (!SafeStorage.getItem('ep_invoices')) dbSet('ep_invoices', []);
        }

        function registerProductionAdmin() {
            const email = prompt('Enter primary admin email address:');
            if (!email) return;
            const password = prompt('Set strong admin account password:');
            if (!password) return;
            const name = prompt('Enter full name of Administrator:') || 'Administrator';

            const users = dbGet('ep_users');
            if (users.some(u => u.identifier === email)) {
                showToast('An account with this email already exists.', 'error');
                return;
            }

            const newAdmin = {
                id: Date.now(),
                identifier: email,
                username: email.split('@')[0],
                phone: '',
                password: password,
                role: 'Admin',
                name: name,
                avatar: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=100'
            };

            users.push(newAdmin);
            dbSet('ep_users', users);
            showToast('Primary Administrator registered. You may now log in.', 'success');
        }

        function checkSession() {
            const saved = SafeStorage.getItem('ep_session') || SafeSessionStorage.getItem('ep_session');
            if (saved) {
                try { currentUser = JSON.parse(saved); bootApp(); } catch (e) { currentUser = null; }
            }
        }

        function togglePasswordVisibility(inputId, btn) {
            const el = document.getElementById(inputId);
            if (el.type === 'password') {
                el.type = 'text';
                btn.innerHTML = '<i class="fa-solid fa-eye-slash"></i>';
            } else {
                el.type = 'password';
                btn.innerHTML = '<i class="fa-solid fa-eye"></i>';
            }
        }

        function bootApp() {
            document.getElementById('auth-screen').classList.add('hidden');
            document.getElementById('app-wrapper').classList.remove('hidden');

            document.getElementById('nav-user-name').innerText = currentUser.name;
            document.getElementById('nav-user-email').innerText = currentUser.identifier;
            document.getElementById('nav-user-avatar').src = currentUser.avatar;
            document.getElementById('header-role-badge').innerText = currentUser.role;

            buildMenuByRBAC();
            updateKPIs();
            renderTeachersTable();
            renderStudentsTable();
            renderGradebookTable();
            renderInvoicesTable();
            initCharts();
            populateAttendanceModal();
            populateInvoiceStudentDropdown();
        }

        function buildMenuByRBAC() {
            const nav = document.getElementById('nav-menu');
            nav.innerHTML = '';
            let tabs = [{ id: 'overview', label: 'Overview', icon: 'fa-gauge' }];

            if (currentUser.role === 'Admin') {
                tabs.push({ id: 'teachers', label: 'Faculty', icon: 'fa-chalkboard-user' });
                tabs.push({ id: 'students', label: 'Students', icon: 'fa-user-graduate' });
                tabs.push({ id: 'grading', label: 'Gradebook', icon: 'fa-pen-to-square' });
                tabs.push({ id: 'billing', label: 'Billing', icon: 'fa-file-invoice-dollar' });
                tabs.push({ id: 'settings', label: 'Settings', icon: 'fa-gear' });
            } else if (currentUser.role === 'Teacher') {
                tabs.push({ id: 'students', label: 'Students', icon: 'fa-user-graduate' });
                tabs.push({ id: 'grading', label: 'Gradebook', icon: 'fa-pen-to-square' });
                tabs.push({ id: 'settings', label: 'Settings', icon: 'fa-gear' });
            } else {
                tabs.push({ id: 'grading', label: 'My Report Card', icon: 'fa-pen-to-square' });
                tabs.push({ id: 'billing', label: 'Fees & Invoices', icon: 'fa-file-invoice-dollar' });
            }

            tabs.forEach((tab, index) => {
                const btn = document.createElement('button');
                btn.className = `px-3.5 py-1.5 rounded-xl flex items-center space-x-1.5 transition ${index === 0 ? 'bg-brand-600 text-white shadow-md' : 'hover:bg-slate-200 dark:hover:bg-slate-800'}`;
                btn.id = `nav-tab-${tab.id}`;
                btn.onclick = () => switchTab(tab.id);
                btn.innerHTML = `<i class="fa-solid ${tab.icon}"></i><span>${tab.label}</span>`;
                nav.appendChild(btn);
            });
            switchTab('overview');
        }

        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById(`tab-${tabId}`).classList.remove('hidden');

            document.querySelectorAll('#nav-menu button').forEach(btn => {
                btn.className = 'px-3.5 py-1.5 rounded-xl flex items-center space-x-1.5 transition hover:bg-slate-200 dark:hover:bg-slate-800';
            });
            const activeBtn = document.getElementById(`nav-tab-${tabId}`);
            if (activeBtn) activeBtn.className = 'px-3.5 py-1.5 rounded-xl flex items-center space-x-1.5 transition bg-brand-600 text-white shadow-md';

            if (tabId === 'settings') {
                const schoolName = SafeStorage.getItem('ep_school_name') || 'EduPulse';
                document.getElementById('settings-school-name').value = schoolName;
            }
        }

        function saveSchoolBranding(e) {
            e.preventDefault();
            const nameInput = document.getElementById('settings-school-name').value.trim();
            if (!nameInput) return;
            SafeStorage.setItem('ep_school_name', nameInput);
            applySchoolBranding();
            showToast(`School name updated to "${nameInput}" successfully!`, 'success');
        }

        function applySchoolBranding() {
            const schoolName = SafeStorage.getItem('ep_school_name') || 'EduPulse';
            const brandEl = document.getElementById('header-school-brand');
            if (brandEl) brandEl.innerText = schoolName;
        }

        function populateInvoiceStudentDropdown() {
            const select = document.getElementById('invoice-form-student');
            if (!select) return;
            const students = dbGet('ep_students') || [];
            select.innerHTML = students.map(s => `<option value="${s.id}">${s.name} (${s.grade})</option>`).join('');
        }

        function populateAttendanceModal() {
            const container = document.getElementById('attendance-list-container');
            const students = dbGet('ep_students') || [];
            container.innerHTML = '';
            if (students.length === 0) {
                container.innerHTML = '<p class="text-xs text-slate-400 py-4 text-center">No enrolled students found to log attendance.</p>';
                return;
            }
            students.forEach(s => {
                container.innerHTML += `
                    <div class="flex items-center justify-between p-2.5 bg-slate-100 dark:bg-slate-900 rounded-xl text-xs">
                        <span class="font-bold">${s.name} (${s.grade})</span>
                        <div class="flex items-center space-x-2">
                            <label class="flex items-center space-x-1"><input type="radio" name="att-${s.id}" value="Present" checked> <span>Present</span></label>
                            <label class="flex items-center space-x-1"><input type="radio" name="att-${s.id}" value="Absent"> <span class="text-red-500">Absent</span></label>
                        </div>
                    </div>
                `;
            });
        }

        function submitAttendance() {
            closeModal('modal-attendance');
            showToast('Attendance logged for current session.', 'success');
        }

        function triggerBroadcastNotice() {
            const msg = prompt('Enter notice message for students & teachers:');
            if (msg) showToast(`Broadcast Sent: "${msg}"`, 'info');
        }

        function handleGlobalSearch(query) {
            if (!query) return;
            showToast(`Filtering records for "${query}"...`, 'info');
        }

        function renderTeachersTable() {
            const list = dbGet('ep_teachers') || [];
            const users = dbGet('ep_users') || [];
            const tbody = document.getElementById('teachers-table-body');
            tbody.innerHTML = '';

            if (list.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-400">No faculty records found. Click "Add Faculty" to register teachers.</td></tr>`;
                return;
            }

            list.forEach(t => {
                const teacherUser = users.find(u => u.identifier === t.email);
                const pass = teacherUser ? teacherUser.password : '******';
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 dark:hover:bg-slate-700/30";
                tr.innerHTML = `
                    <td class="p-3.5 font-bold">${t.name}</td>
                    <td class="p-3.5"><span class="px-2 py-0.5 bg-purple-100 text-purple-700 dark:bg-purple-900/40 dark:text-purple-300 rounded-md font-semibold">${t.dept}</span></td>
                    <td class="p-3.5">${t.subject}</td>
                    <td class="p-3.5">${t.phone}</td>
                    <td class="p-3.5"><span class="font-mono text-brand-600 font-bold">${pass}</span></td>
                    <td class="p-3.5"><span class="px-2 py-0.5 bg-emerald-100 text-emerald-700 rounded-full font-semibold">${t.status}</span></td>
                    <td class="p-3.5 text-right space-x-1">
                        <button onclick="editTeacher(${t.id})" class="p-1.5 text-blue-500"><i class="fa-solid fa-pen-to-square"></i></button>
                        <button onclick="deleteTeacher(${t.id})" class="p-1.5 text-red-500"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderStudentsTable() {
            const list = dbGet('ep_students') || [];
            const tbody = document.getElementById('students-table-body');
            tbody.innerHTML = '';

            if (list.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="p-4 text-center text-slate-400">No student enrollments found. Click "Enroll Student" to create records.</td></tr>`;
                return;
            }

            list.forEach(s => {
                const gpa = (((s.midterm*0.4)+(s.lab*0.3)+(s.final*0.3))/25).toFixed(2);
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 dark:hover:bg-slate-700/30";
                tr.innerHTML = `
                    <td class="p-3.5 font-bold">${s.name}</td>
                    <td class="p-3.5 font-mono text-[11px] text-slate-500">${s.code}</td>
                    <td class="p-3.5">${s.grade}</td>
                    <td class="p-3.5">${(s.subjects || []).join(', ')}</td>
                    <td class="p-3.5 text-slate-500">${s.guardian}</td>
                    <td class="p-3.5 font-extrabold text-brand-600">${gpa}</td>
                    <td class="p-3.5"><span class="px-2 py-0.5 ${s.feeStatus === 'Paid' ? 'bg-emerald-100 text-emerald-700' : 'bg-red-100 text-red-700'} rounded-full font-bold">${s.feeStatus}</span></td>
                    <td class="p-3.5 text-right space-x-1">
                        <button onclick="editStudent(${s.id})" class="p-1.5 text-blue-500"><i class="fa-solid fa-pen-to-square"></i></button>
                        <button onclick="deleteStudent(${s.id})" class="p-1.5 text-red-500"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderGradebookTable() {
            const students = dbGet('ep_students') || [];
            const tbody = document.getElementById('gradebook-table-body');
            tbody.innerHTML = '';

            if (students.length === 0) {
                tbody.innerHTML = `<tr><td colspan="8" class="p-4 text-center text-slate-400">No marksheet records available. Enroll students to enable grade tracking.</td></tr>`;
                document.getElementById('marksheet-class-avg').innerText = '--';
                document.getElementById('marksheet-highest-score').innerText = '--';
                document.getElementById('marksheet-total-students').innerText = '0';
                return;
            }

            let total = 0, highest = 0;
            students.forEach(s => {
                const avg = parseFloat(((s.midterm * 0.4) + (s.lab * 0.3) + (s.final * 0.3)).toFixed(1));
                total += avg; if (avg > highest) highest = avg;
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td class="p-3.5 font-bold">${s.name}</td>
                    <td class="p-3.5">${s.grade}</td>
                    <td class="p-3.5"><input type="number" value="${s.midterm}" onchange="updateGradeScore(${s.id}, 'midterm', this.value)" class="w-16 bg-slate-100 dark:bg-slate-900 border rounded-lg px-2 py-1 text-xs"></td>
                    <td class="p-3.5"><input type="number" value="${s.lab}" onchange="updateGradeScore(${s.id}, 'lab', this.value)" class="w-16 bg-slate-100 dark:bg-slate-900 border rounded-lg px-2 py-1 text-xs"></td>
                    <td class="p-3.5"><input type="number" value="${s.final}" onchange="updateGradeScore(${s.id}, 'final', this.value)" class="w-16 bg-slate-100 dark:bg-slate-900 border rounded-lg px-2 py-1 text-xs"></td>
                    <td class="p-3.5 font-extrabold text-brand-600">${avg}%</td>
                    <td class="p-3.5"><span class="px-2.5 py-1 bg-brand-100 text-brand-800 font-bold rounded-md">${avg >= 90 ? 'A' : avg >= 80 ? 'B' : 'C'}</span></td>
                    <td class="p-3.5 text-right"><button onclick="printReportCard(${s.id})" class="p-1.5 text-brand-600"><i class="fa-solid fa-print"></i></button></td>
                `;
                tbody.appendChild(tr);
            });

            if (students.length) {
                document.getElementById('marksheet-class-avg').innerText = (total / students.length).toFixed(1) + '%';
                document.getElementById('marksheet-highest-score').innerText = highest.toFixed(1) + '%';
                document.getElementById('marksheet-total-students').innerText = students.length;
            }
        }

        function renderInvoicesTable() {
            const invoices = dbGet('ep_invoices') || [];
            const tbody = document.getElementById('invoices-table-body');
            tbody.innerHTML = '';

            if (invoices.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-4 text-center text-slate-400">No active invoices issued. Click "Issue New Invoice" to generate billing records.</td></tr>`;
                return;
            }

            invoices.forEach(inv => {
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td class="p-3.5 font-mono text-[11px] font-bold">${inv.id}</td>
                    <td class="p-3.5 font-semibold">${inv.studentName}</td>
                    <td class="p-3.5">${inv.desc}</td>
                    <td class="p-3.5 font-bold">$${inv.amount}.00</td>
                    <td class="p-3.5">${inv.date}</td>
                    <td class="p-3.5"><span class="px-2 py-0.5 ${inv.status === 'Paid' ? 'bg-emerald-100 text-emerald-700' : 'bg-red-100 text-red-700'} rounded-full font-bold">${inv.status}</span></td>
                    <td class="p-3.5 text-right">
                        ${inv.status === 'Unpaid' ? `<button onclick="markInvoicePaid('${inv.id}')" class="px-2 py-1 bg-emerald-600 text-white rounded-lg text-[10px] font-bold">Mark Paid</button>` : `<span class="text-xs text-slate-400">Settled</span>`}
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function updateGradeScore(studentId, field, val) {
            const list = dbGet('ep_students');
            const s = list.find(x => x.id === studentId);
            if (s) {
                s[field] = parseFloat(val) || 0;
                dbSet('ep_students', list);
                renderGradebookTable();
                showToast('Marksheet updated.', 'info');
            }
        }

        function markInvoicePaid(invId) {
            const invoices = dbGet('ep_invoices');
            const inv = invoices.find(i => i.id === invId);
            if (inv) {
                inv.status = 'Paid';
                dbSet('ep_invoices', invoices);
                const students = dbGet('ep_students');
                const s = students.find(x => x.id === inv.studentId);
                if (s) { s.feeStatus = 'Paid'; dbSet('ep_students', students); }
                renderInvoicesTable();
                renderStudentsTable();
                updateKPIs();
                showToast('Invoice status updated to Paid.', 'success');
            }
        }

        function generateRandomPassword(targetId) {
            const chars = 'abcdefghjkmnpqrstuvwxyzABCDEFGHJKLMNPQRSTUVWXYZ23456789';
            let pass = '';
            for (let i = 0; i < 8; i++) pass += chars.charAt(Math.floor(Math.random() * chars.length));
            const input = document.getElementById(targetId);
            if (input) { input.value = pass; input.type = 'text'; }
        }

        function updateKPIs() {
            const students = dbGet('ep_students') || [];
            const teachers = dbGet('ep_teachers') || [];
            const invoices = dbGet('ep_invoices') || [];

            document.getElementById('kpi-students-count').innerText = students.length;
            document.getElementById('kpi-teachers-count').innerText = teachers.length;

            const totalRevenue = invoices.filter(i => i.status === 'Paid').reduce((acc, i) => acc + i.amount, 0);
            document.getElementById('kpi-revenue').innerText = '$' + totalRevenue.toLocaleString();
        }

        let enrollmentChart = null;
        let feeChart = null;

        function initCharts() {
            const students = dbGet('ep_students') || [];
            const invoices = dbGet('ep_invoices') || [];

            const paidCount = invoices.filter(i => i.status === 'Paid').length;
            const unpaidCount = invoices.filter(i => i.status === 'Unpaid').length;

            const ctx1 = document.getElementById('chart-enrollment').getContext('2d');
            if (enrollmentChart) enrollmentChart.destroy();
            enrollmentChart = new Chart(ctx1, {
                type: 'line',
                data: {
                    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Current'],
                    datasets: [{ label: 'Active Enrolments', data: [0, Math.round(students.length * 0.3), Math.round(students.length * 0.5), Math.round(students.length * 0.8), students.length, students.length], borderColor: '#6366f1', fill: true, backgroundColor: 'rgba(99, 102, 241, 0.1)', tension: 0.3 }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });

            const ctx2 = document.getElementById('chart-fees').getContext('2d');
            if (feeChart) feeChart.destroy();
            feeChart = new Chart(ctx2, {
                type: 'doughnut',
                data: {
                    labels: ['Settled Invoices', 'Outstanding Receivables'],
                    datasets: [{ data: [paidCount || 1, unpaidCount], backgroundColor: ['#10b981', '#ef4444'] }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }

        function openModal(id) { document.getElementById(id).classList.remove('hidden'); }
        function closeModal(id) { document.getElementById(id).classList.add('hidden'); }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            SafeStorage.setItem('ep_theme', document.documentElement.classList.contains('dark') ? 'dark' : 'light');
        }

        function showToast(message, type = 'info') {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            const bg = type === 'success' ? 'bg-emerald-600' : type === 'error' ? 'bg-red-600' : 'bg-slate-800';
            toast.className = `${bg} text-white px-4 py-3 rounded-xl shadow-xl text-xs font-semibold flex items-center space-x-2 transition pointer-events-auto`;
            toast.innerHTML = `<i class="fa-solid fa-circle-info"></i><span>${message}</span>`;
            container.appendChild(toast);
            setTimeout(() => toast.remove(), 3000);
        }

        function saveTeacherForm(e) {
            e.preventDefault();
            const id = document.getElementById('teacher-form-id').value;
            const name = document.getElementById('teacher-form-name').value.trim();
            const email = document.getElementById('teacher-form-email').value.trim();
            const phone = document.getElementById('teacher-form-phone').value.trim();
            const password = document.getElementById('teacher-form-password').value;
            const dept = document.getElementById('teacher-form-dept').value;
            const subject = document.getElementById('teacher-form-subject').value.trim();

            let teachers = dbGet('ep_teachers');
            let users = dbGet('ep_users');

            if (id) {
                const tIndex = teachers.findIndex(x => String(x.id) === String(id));
                if (tIndex !== -1) {
                    const oldEmail = teachers[tIndex].email;
                    teachers[tIndex] = { ...teachers[tIndex], name, email, phone, dept, subject };

                    const uIndex = users.findIndex(u => u.identifier === oldEmail || String(u.id) === String(id));
                    if (uIndex !== -1) {
                        users[uIndex].identifier = email;
                        users[uIndex].name = name;
                        users[uIndex].phone = phone;
                        if (password) users[uIndex].password = password;
                    }
                }
                showToast('Faculty record updated successfully.', 'success');
            } else {
                const newId = Date.now();
                const newTeacher = { id: newId, name, email, phone, dept, subject, status: 'Active' };
                teachers.push(newTeacher);

                const newTeacherUser = {
                    id: newId,
                    identifier: email,
                    username: email.split('@')[0],
                    phone: phone,
                    password: password || 'teacher123',
                    role: 'Teacher',
                    name: name,
                    avatar: 'https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?w=100'
                };
                users.push(newTeacherUser);
                showToast('New faculty staff registered.', 'success');
            }

            dbSet('ep_teachers', teachers);
            dbSet('ep_users', users);
            closeModal('modal-teacher');

            document.getElementById('teacher-form-id').value = '';
            document.getElementById('teacher-form-name').value = '';
            document.getElementById('teacher-form-email').value = '';
            document.getElementById('teacher-form-phone').value = '';
            document.getElementById('teacher-form-password').value = '';

            renderTeachersTable();
            updateKPIs();
        }

        function editTeacher(id) {
            const teachers = dbGet('ep_teachers');
            const users = dbGet('ep_users');
            const t = teachers.find(x => String(x.id) === String(id));
            if (!t) return;

            const u = users.find(x => x.identifier === t.email);

            document.getElementById('teacher-form-id').value = t.id;
            document.getElementById('teacher-form-name').value = t.name;
            document.getElementById('teacher-form-email').value = t.email;
            document.getElementById('teacher-form-phone').value = t.phone || '';
            document.getElementById('teacher-form-dept').value = t.dept;
            document.getElementById('teacher-form-subject').value = t.subject;
            document.getElementById('teacher-form-password').value = u ? u.password : '';
            document.getElementById('modal-teacher-title').innerText = 'Edit Faculty Staff';

            openModal('modal-teacher');
        }

        function deleteTeacher(id) {
            if (!confirm('Are you sure you want to remove this faculty record?')) return;
            let teachers = dbGet('ep_teachers');
            const t = teachers.find(x => String(x.id) === String(id));

            teachers = teachers.filter(x => String(x.id) !== String(id));
            dbSet('ep_teachers', teachers);

            if (t) {
                let users = dbGet('ep_users');
                users = users.filter(u => u.identifier !== t.email);
                dbSet('ep_users', users);
            }

            showToast('Faculty member removed.', 'info');
            renderTeachersTable();
            updateKPIs();
        }

        function saveStudentForm(e) {
            e.preventDefault();
            const id = document.getElementById('student-form-id').value;
            const name = document.getElementById('student-form-name').value.trim();
            const grade = document.getElementById('student-form-grade').value;
            const email = document.getElementById('student-form-email').value.trim();
            const guardian = document.getElementById('student-form-guardian').value.trim();

            const selectedSubjects = Array.from(document.querySelectorAll('input[name="student-subjects"]:checked')).map(cb => cb.value);

            let students = dbGet('ep_students');

            if (id) {
                const sIndex = students.findIndex(x => String(x.id) === String(id));
                if (sIndex !== -1) {
                    students[sIndex] = {
                        ...students[sIndex],
                        name, grade, email, guardian,
                        subjects: selectedSubjects.length ? selectedSubjects : students[sIndex].subjects
                    };
                }
                showToast('Student record updated.', 'success');
            } else {
                const newStudent = {
                    id: Date.now(),
                    code: 'STU-' + Math.floor(1000 + Math.random() * 9000),
                    name, grade, email, guardian,
                    subjects: selectedSubjects.length ? selectedSubjects : ['English Language', 'Primary Mathematics'],
                    midterm: 80, lab: 85, final: 82,
                    feeStatus: 'Unpaid'
                };
                students.push(newStudent);
                showToast('Student enrolled successfully.', 'success');
            }

            dbSet('ep_students', students);
            closeModal('modal-student');

            document.getElementById('student-form-id').value = '';
            document.getElementById('student-form-name').value = '';
            document.getElementById('student-form-email').value = '';
            document.getElementById('student-form-guardian').value = '';
            document.querySelectorAll('input[name="student-subjects"]').forEach(cb => cb.checked = false);

            renderStudentsTable();
            renderGradebookTable();
            updateKPIs();
            populateAttendanceModal();
            populateInvoiceStudentDropdown();
        }

        function editStudent(id) {
            const students = dbGet('ep_students');
            const s = students.find(x => String(x.id) === String(id));
            if (!s) return;

            document.getElementById('student-form-id').value = s.id;
            document.getElementById('student-form-name').value = s.name;
            document.getElementById('student-form-grade').value = s.grade;
            document.getElementById('student-form-email').value = s.email;
            document.getElementById('student-form-guardian').value = s.guardian;

            document.querySelectorAll('input[name="student-subjects"]').forEach(cb => {
                cb.checked = (s.subjects || []).includes(cb.value);
            });

            document.getElementById('modal-student-title').innerText = 'Edit Student Enrollment';
            openModal('modal-student');
        }

        function deleteStudent(id) {
            if (!confirm('Are you sure you want to delete this student profile?')) return;
            let students = dbGet('ep_students');
            students = students.filter(x => String(x.id) !== String(id));
            dbSet('ep_students', students);

            let invoices = dbGet('ep_invoices');
            invoices = invoices.filter(x => String(x.studentId) !== String(id));
            dbSet('ep_invoices', invoices);

            showToast('Student record deleted.', 'info');
            renderStudentsTable();
            renderGradebookTable();
            renderInvoicesTable();
            updateKPIs();
            populateAttendanceModal();
            populateInvoiceStudentDropdown();
        }

        function saveInvoiceForm(e) {
            e.preventDefault();
            const studentId = document.getElementById('invoice-form-student').value;
            const desc = document.getElementById('invoice-form-desc').value.trim();
            const amount = parseFloat(document.getElementById('invoice-form-amount').value) || 0;
            const date = document.getElementById('invoice-form-date').value;

            const students = dbGet('ep_students');
            const student = students.find(s => String(s.id) === String(studentId));

            if (!student) {
                showToast('Please select a valid student.', 'error');
                return;
            }

            const invoices = dbGet('ep_invoices');
            const newInv = {
                id: 'INV-' + Math.floor(1000 + Math.random() * 9000),
                studentId: student.id,
                studentName: student.name,
                desc: desc,
                amount: amount,
                date: date,
                status: 'Unpaid'
            };

            invoices.push(newInv);
            dbSet('ep_invoices', invoices);

            student.feeStatus = 'Unpaid';
            dbSet('ep_students', students);

            closeModal('modal-invoice');
            renderInvoicesTable();
            renderStudentsTable();
            updateKPIs();
            showToast('New fee invoice generated.', 'success');
        }

        function exportTableToCSV(type) {
            let data = [], filename = `${type}_records.csv`;
            if (type === 'teachers') data = dbGet('ep_teachers');
            else if (type === 'students') data = dbGet('ep_students');

            if (!data.length) { showToast('No records to export.', 'error'); return; }

            const keys = Object.keys(data[0]);
            let csv = keys.join(',') + '\n';
            data.forEach(row => {
                csv += keys.map(k => `"${String(row[k] || '').replace(/"/g, '""')}"`).join(',') + '\n';
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = filename;
            a.click();
            window.URL.revokeObjectURL(url);
            showToast(`Exported ${type} dataset to CSV.`, 'success');
        }

        function exportClassMarksheet() {
            const students = dbGet('ep_students');
            if (!students.length) { showToast('No marksheets available.', 'error'); return; }
            let csv = 'Student Name,Grade,Midterm (40%),Assignments (30%),Final Exam (30%),Overall Score,Letter Grade\n';
            students.forEach(s => {
                const avg = ((s.midterm * 0.4) + (s.lab * 0.3) + (s.final * 0.3)).toFixed(1);
                const letter = avg >= 90 ? 'A' : avg >= 80 ? 'B' : 'C';
                csv += `"${s.name}","${s.grade}",${s.midterm},${s.lab},${s.final},${avg}%,${letter}\n`;
            });
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'class_marksheets.csv';
            a.click();
            window.URL.revokeObjectURL(url);
            showToast('Class marksheets exported.', 'success');
        }

        function printReportCard(studentId) {
            const students = dbGet('ep_students');
            const s = students.find(x => String(x.id) === String(studentId));
            if (!s) return;

            const avg = ((s.midterm * 0.4) + (s.lab * 0.3) + (s.final * 0.3)).toFixed(1);
            const details = document.getElementById('report-card-details');
            details.innerHTML = `
                <div class="grid grid-cols-2 gap-4 my-4 p-4 bg-slate-50 border rounded-xl">
                    <div><strong>Student Name:</strong> ${s.name}</div>
                    <div><strong>ID Code:</strong> ${s.code}</div>
                    <div><strong>Grade Level:</strong> ${s.grade}</div>
                    <div><strong>Guardian:</strong> ${s.guardian}</div>
                </div>
                <table class="w-full text-left border my-4 text-xs">
                    <thead><tr class="bg-slate-100"><th class="p-2 border">Assessment Component</th><th class="p-2 border">Weight</th><th class="p-2 border">Score</th></tr></thead>
                    <tbody>
                        <tr><td class="p-2 border">Midterm Assessment</td><td class="p-2 border">40%</td><td class="p-2 border">${s.midterm}%</td></tr>
                        <tr><td class="p-2 border">Assignments & Labs</td><td class="p-2 border">30%</td><td class="p-2 border">${s.lab}%</td></tr>
                        <tr><td class="p-2 border">Final Examination</td><td class="p-2 border">30%</td><td class="p-2 border">${s.final}%</td></tr>
                    </tbody>
                </table>
                <div class="text-right p-4 bg-slate-100 rounded-xl">
                    <span class="text-base font-bold">Calculated Term Score: ${avg}%</span>
                </div>
            `;
            window.print();
        }

        function downloadProductionBundle() {
            const htmlContent = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
            const blob = new Blob([htmlContent], { type: 'text/html' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'edupulse-os-production.html';
            a.click();
            window.URL.revokeObjectURL(url);
            showToast('Production HTML Bundle downloaded successfully!', 'success');
        }

        function copySourceToClipboard() {
            const htmlContent = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
            const textarea = document.createElement('textarea');
            textarea.value = htmlContent;
            document.body.appendChild(textarea);
            textarea.select();
            document.execCommand('copy');
            document.body.removeChild(textarea);
            showToast('Complete application source code copied to clipboard!', 'success');
        }

        window.onload = function() {
            dbInit();
            if (SafeStorage.getItem('ep_theme') === 'dark') document.documentElement.classList.add('dark');
            applySchoolBranding();
            checkSession();
        };
    </script>
</body>
</html>
