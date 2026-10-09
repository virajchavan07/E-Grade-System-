# E-Grade-System-https://
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Grade System</title>
    <!-- Tailwind CSS (Styling के लिए) -->
    <script src="https://tailwindcss.com"></script>
    <!-- Lucide Icons (Icons के लिए) -->
    <script src="https://unpkg.com"></script>
    <style>
        .custom-green-dark { color: #123524; }
        .custom-green-bg { background-color: #123524; }
        .custom-green-light { background-color: #EBF3E8; }
    </style>
</head>
<body class="bg-gray-50 font-sans antialiased">

    <!-- 1. LOGIN PAGE (लॉगिन पेज) -->
    <div id="login-page" class="min-h-screen flex items-center justify-center custom-green-light p-4">
        <div class="bg-white rounded-2xl shadow-xl p-8 max-w-sm w-full border border-gray-100">
            <div class="flex items-center gap-2 mb-8">
                <div class="p-2 bg-emerald-100 rounded-lg text-emerald-800">
                    <i data-lucide="graduation-cap" class="w-6 h-6"></i>
                </div>
                <span class="text-xl font-bold custom-green-dark">E-Grade System</span>
            </div>

            <h2 class="text-2xl font-bold custom-green-dark mb-1">Welcome back.</h2>
            <p class="text-gray-500 text-sm mb-6">Sign in to manage student grades & academic progress.</p>

            <form id="login-form" onsubmit="handleLogin(event)">
                <div class="mb-4">
                    <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Email</label>
                    <input type="email" id="login-email" required value="admin@egrade.com" class="w-full px-4 py-2.5 rounded-xl border border-gray-300 focus:outline-none focus:ring-2 focus:ring-emerald-700 text-sm">
                </div>
                <div class="mb-2">
                    <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Password</label>
                    <input type="password" id="login-password" required value="123456" class="w-full px-4 py-2.5 rounded-xl border border-gray-300 focus:outline-none focus:ring-2 focus:ring-emerald-700 text-sm">
                </div>
                <div class="text-right mb-6">
                    <a href="#" class="text-xs text-emerald-700 font-medium hover:underline">Forgot password?</a>
                </div>

                <button type="submit" class="w-full py-3 custom-green-bg text-white font-semibold rounded-xl hover:opacity-90 transition text-sm shadow-md">
                    Sign in
                </button>
            </form>
        </div>
    </div>

    <!-- 2. DASHBOARD (डैशबोर्ड - लॉगिन के बाद दिखेगा) -->
    <div id="app-dashboard" class="hidden min-h-screen flex flex-col md:flex-row">
        
        <!-- SIDEBAR (साइडबार) -->
        <aside class="w-full md:w-64 custom-green-bg text-white flex flex-col justify-between p-4 shrink-0">
            <div>
                <div class="flex items-center gap-2 mb-8 px-2 py-3 border-b border-emerald-950">
                    <i data-lucide="graduation-cap" class="w-6 h-6 text-emerald-400"></i>
                    <span class="text-lg font-bold tracking-wide">E-Grade System</span>
                </div>
                <nav class="space-y-1">
                    <a href="#" class="flex items-center gap-3 px-3 py-2.5 rounded-xl bg-emerald-900 text-emerald-100 text-sm font-medium">
                        <i data-lucide="layout-dashboard" class="w-4 h-4"></i> Dashboard
                    </a>
                    <a href="#" class="flex items-center gap-3 px-3 py-2.5 rounded-xl text-emerald-300 hover:bg-emerald-900/50 hover:text-white text-sm font-medium transition">
                        <i data-lucide="users" class="w-4 h-4"></i> Students
                    </a>
                </nav>
            </div>
            
            <button onclick="handleLogout()" class="flex items-center gap-3 px-3 py-2.5 mt-8 rounded-xl text-rose-300 hover:bg-rose-950/30 text-sm font-medium transition w-full text-left">
                <i data-lucide="log-out" class="w-4 h-4"></i> Logout
            </button>
        </aside>

        <!-- MAIN CONTENT (मुख्य सामग्री) -->
        <main class="flex-1 p-4 md:p-8 overflow-y-auto">
            <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4 mb-8">
                <div>
                    <h1 class="text-2xl font-bold custom-green-dark">Student Grade Tracker</h1>
                    <p class="text-sm text-gray-500">Manage student scores and academic performance efficiently.</p>
                </div>
                <button onclick="openModal()" class="flex items-center justify-center gap-2 px-4 py-2.5 custom-green-bg text-white rounded-xl text-sm font-medium hover:opacity-90 shadow transition">
                    <i data-lucide="plus" class="w-4 h-4"></i> Add Record
                </button>
            </div>

            <!-- STATS CARDS (आंकड़े) -->
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
                <div class="bg-white p-4 rounded-xl border border-gray-200 shadow-sm">
                    <span class="text-xs font-semibold text-gray-400 uppercase block mb-1">Total Students</span>
                    <span id="stat-total" class="text-2xl font-bold custom-green-dark">0</span>
                </div>
                <div class="bg-white p-4 rounded-xl border border-gray-200 shadow-sm">
                    <span class="text-xs font-semibold text-gray-400 uppercase block mb-1">Class Average</span>
                    <span id="stat-avg" class="text-2xl font-bold custom-green-dark">0.0</span>
                </div>
                <div class="bg-white p-4 rounded-xl border border-gray-200 shadow-sm">
                    <span class="text-xs font-semibold text-gray-400 uppercase block mb-1">Passing Rate</span>
                    <span id="stat-passing" class="text-2xl font-bold custom-green-dark">0%</span>
                </div>
                <div class="bg-white p-4 rounded-xl border border-gray-200 shadow-sm">
                    <span class="text-xs font-semibold text-gray-400 uppercase block mb-1">Highest Score</span>
                    <span id="stat-highest" class="text-2xl font-bold custom-green-dark">0</span>
                </div>
            </div>

            <!-- TABLE (टेबल) -->
            <div class="bg-white rounded-xl border border-gray-200 shadow-sm overflow-hidden">
                <div class="overflow-x-auto">
                    <table class="w-full text-left border-collapse text-sm">
                        <thead>
                            <tr class="bg-gray-50 border-b border-gray-200 text-gray-400 font-semibold text-xs uppercase">
                                <th class="p-4">Student Name</th>
                                <th class="p-4">Subject</th>
                                <th class="p-4">Score</th>
                                <th class="p-4">Grade</th>
                                <th class="p-4 text-right">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="student-table-body" class="divide-y divide-gray-100 text-gray-700">
                            <!-- डेटा यहाँ लोड होगा -->
                        </tbody>
                    </table>
                </div>
            </div>
        </main>
    </div>

    <!-- 3. MODAL WINDOW (नया रिकॉर्ड जोड़ने के लिए पॉपअप) -->
    <div id="record-modal" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/50 backdrop-blur-sm">
        <div class="bg-white rounded-2xl w-full max-w-md shadow-2xl overflow-hidden border border-gray-100">
            <div class="p-5 border-b border-gray-100 flex justify-between items-center bg-gray-50/50">
                <h3 class="font-bold text-gray-800 flex items-center gap-2">
                    <i data-lucide="plus-circle" class="w-5 h-5 text-emerald-700"></i> Add Student Record
                </h3>
                <button onclick="closeModal()" class="text-gray-400 hover:text-gray-600">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>

            <form id="record-form" onsubmit="handleRecordSubmit(event)" class="p-5 space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Student Full Name</label>
                    <input type="text" id="input-name" required placeholder="जैसे: Rahul Kumar" class="w-full px-3 py-2 border rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-700 text-sm">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Subject</label>
                    <select id="input-subject" class="w-full px-3 py-2 border rounded-xl bg-white focus:outline-none focus:ring-2 focus:ring-emerald-700 text-sm">
                        <option value="Mathematics">Mathematics</option>
                        <option value="Computer Science">Computer Science</option>
                        <option value="Physics">Physics</option>
                        <option value="Chemistry">Chemistry</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-gray-600 uppercase mb-1">Score (0-100)</label>
                    <input type="number" id="input-score" required min="0" max="100" placeholder="जैसे: 85" class="w-full px-3 py-2 border rounded-xl focus:outline-none focus:ring-2 focus:ring-emerald-700 text-sm">
                </div>

                <div class="flex gap-3 pt-3">
                    <button type="button" onclick="closeModal()" class="flex-1 py-2.5 border border-gray-300 text-gray-700 text-sm font-medium rounded-xl hover:bg-gray-50">
                        Cancel
l
