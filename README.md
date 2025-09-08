<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GameLog</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka+One:wght@400&family=Inter:wght@400;500;600;700&display=swap');
        
        .basketball-font { font-family: 'Fredoka One', cursive; }
        .main-font { font-family: 'Inter', sans-serif; }
        
        .basketball-bg {
            background: linear-gradient(135deg, #ff6b35 0%, #f7931e 100%);
        }
        
        .court-pattern {
            background-image: 
                radial-gradient(circle at 25% 25%, rgba(255,255,255,0.1) 2px, transparent 2px),
                radial-gradient(circle at 75% 75%, rgba(255,255,255,0.1) 2px, transparent 2px);
            background-size: 50px 50px;
        }
        
        .bounce {
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }
        
        .stat-card {
            background: linear-gradient(145deg, #ffffff 0%, #f8fafc 100%);
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }
        
        .achievement-glow {
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.5);
        }
    </style>
</head>
<body class="main-font bg-gray-50 min-h-screen">
    <!-- L8sSa67 -->
    <nav class="basketball-bg court-pattern shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center py-4">
                <div class="flex items-center space-x-3">
                    <div class="text-4xl bounce">🏀</div>
                    <h1 class="basketball-font text-2xl md:text-3xl text-black">GameLog</h1>
                </div>
                <div class="flex space-x-4">
                    <button onclick="showPage('home')" class="nav-btn bg-white/20 hover:bg-white/30 text-white px-4 py-2 rounded-lg font-semibold transition-all">
                        🏠 Home
                    </button>
                    <button onclick="showPage('history')" class="nav-btn bg-white/20 hover:bg-white/30 text-white px-4 py-2 rounded-lg font-semibold transition-all">
                        📊 Game History
                    </button>
                    <button onclick="showPage('admin')" class="nav-btn bg-white/20 hover:bg-white/30 text-white px-4 py-2 rounded-lg font-semibold transition-all">
                        ⚙️ Admin
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Home Page -->
    <div id="homePage" class="page">
        <div class="max-w-7xl mx-auto px-4 py-8">
            <!-- Welcome Section -->
            <div class="text-center mb-8">
                <h2 class="basketball-font text-4xl text-gray-800 mb-4">Welcome Back! 🌟</h2>
                <p class="text-xl text-gray-600">Keep crushing it on the court!</p>
            </div>

            <!-- Overall Stats Cards -->
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-6 mb-8">
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🏀</div>
                    <div class="text-2xl font-bold text-orange-600" id="totalPoints">0</div>
                    <div class="text-gray-600 font-medium">Total Points</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🤾</div>
                    <div class="text-2xl font-bold text-blue-600" id="totalRebounds">0</div>
                    <div class="text-gray-600 font-medium">Rebounds</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🎯</div>
                    <div class="text-2xl font-bold text-green-600" id="totalAssists">0</div>
                    <div class="text-gray-600 font-medium">Assists</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🥷</div>
                    <div class="text-2xl font-bold text-purple-600" id="totalSteals">0</div>
                    <div class="text-gray-600 font-medium">Steals</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🏆</div>
                    <div class="text-2xl font-bold text-yellow-600" id="totalGames">0</div>
                    <div class="text-gray-600 font-medium">Games Played</div>
                </div>
            </div>

            <!-- Charts and Progress -->
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
                <!-- Progress Chart -->
                <div class="stat-card rounded-xl p-6">
                    <h3 class="text-xl font-bold text-gray-800 mb-4">📈 Points Progress</h3>
                    <canvas id="progressChart" width="400" height="200"></canvas>
                </div>

                <!-- Recent Games -->
                <div class="stat-card rounded-xl p-6">
                    <h3 class="text-xl font-bold text-gray-800 mb-4">🎮 Recent Games</h3>
                    <div id="recentGames" class="space-y-3">
                        <div class="text-gray-500 text-center py-8">No games recorded yet! Add your first game in the Admin panel.</div>
                    </div>
                </div>
            </div>

            <!-- Achievements -->
            <div class="stat-card rounded-xl p-6 mb-8">
                <h3 class="text-xl font-bold text-gray-800 mb-6">🏅 Achievements</h3>
                <div id="achievements" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                    <!-- Achievements will be populated by JavaScript -->
                </div>
            </div>

            <!-- Practice Calendar -->
            <div class="stat-card rounded-xl p-6">
                <div class="flex justify-between items-center mb-4">
                    <h3 class="text-xl font-bold text-gray-800">📅 This Week's Schedule</h3>
                    <div class="text-sm text-gray-500">Click any day to edit</div>
                </div>
                <div class="grid grid-cols-7 gap-2">
                    <div class="text-center font-semibold text-gray-600 py-2">Sun</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Mon</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Tue</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Wed</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Thu</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Fri</div>
                    <div class="text-center font-semibold text-gray-600 py-2">Sat</div>
                    
                    <div id="day-0" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(0)">
                        <div class="day-number font-semibold">1</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-1" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(1)">
                        <div class="day-number font-semibold">2</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-2" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(2)">
                        <div class="day-number font-semibold">3</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-3" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(3)">
                        <div class="day-number font-semibold">4</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-4" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(4)">
                        <div class="day-number font-semibold">5</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-5" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(5)">
                        <div class="day-number font-semibold">6</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                    <div id="day-6" class="schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all" onclick="editScheduleDay(6)">
                        <div class="day-number font-semibold">7</div>
                        <div class="day-activity text-xs mt-1"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Game History Page -->
    <div id="historyPage" class="page hidden">
        <div class="max-w-7xl mx-auto px-4 py-8">
            <!-- Header -->
            <div class="text-center mb-8">
                <h2 class="basketball-font text-4xl text-gray-800 mb-4">📊 Game History</h2>
                <p class="text-xl text-gray-600">All your basketball games and stats</p>
            </div>

            <!-- Summary Stats -->
            <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🏆</div>
                    <div class="text-2xl font-bold text-green-600" id="totalWins">0</div>
                    <div class="text-gray-600 font-medium">Wins</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">😤</div>
                    <div class="text-2xl font-bold text-red-600" id="totalLosses">0</div>
                    <div class="text-gray-600 font-medium">Losses</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">📈</div>
                    <div class="text-2xl font-bold text-orange-600" id="avgPoints">0</div>
                    <div class="text-gray-600 font-medium">Avg Points</div>
                </div>
                <div class="stat-card rounded-xl p-6 text-center">
                    <div class="text-3xl mb-2">🎯</div>
                    <div class="text-2xl font-bold text-blue-600" id="bestGame">0</div>
                    <div class="text-gray-600 font-medium">Best Game</div>
                </div>
            </div>

            <!-- Games List -->
            <div class="stat-card rounded-xl p-6">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-xl font-bold text-gray-800">All Games</h3>
                    <div class="flex space-x-2">
                        <button onclick="sortGames('date')" class="px-4 py-2 bg-orange-100 text-orange-600 rounded-lg hover:bg-orange-200 transition-all">
                            📅 Sort by Date
                        </button>
                        <button onclick="sortGames('points')" class="px-4 py-2 bg-blue-100 text-blue-600 rounded-lg hover:bg-blue-200 transition-all">
                            🏀 Sort by Points
                        </button>
                    </div>
                </div>
                
                <div id="gamesList" class="space-y-4">
                    <!-- Games will be populated here -->
                </div>
            </div>
        </div>
    </div>

    <!-- Admin Page -->
    <div id="adminPage" class="page hidden">
        <div class="max-w-4xl mx-auto px-4 py-8">
            <!-- Login Form -->
            <div id="loginForm" class="stat-card rounded-xl p-8 max-w-md mx-auto">
                <h2 class="basketball-font text-2xl text-center text-gray-800 mb-6">🔐 Admin Login</h2>
                <div class="space-y-4">
                    <div>
                        <label class="block text-gray-700 font-medium mb-2">Password</label>
                        <input type="password" id="adminPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" placeholder="Enter admin password">
                    </div>
                    <button onclick="login()" class="w-full basketball-bg text-white py-3 rounded-lg font-semibold hover:opacity-90 transition-all">
                        Login
                    </button>
                    <div id="loginError" class="text-red-500 text-center hidden">Incorrect password!</div>
                </div>
            </div>

            <!-- Admin Panel -->
            <div id="adminPanel" class="hidden">
                <div class="text-center mb-8">
                    <h2 class="basketball-font text-3xl text-gray-800 mb-4">⚙️ Admin Panel</h2>
                    <p class="text-gray-600">Add new game stats and track progress</p>
                    <button onclick="logout()" class="mt-4 bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg">Logout</button>
                </div>

                <!-- Add Game Form -->
                <div class="stat-card rounded-xl p-8">
                    <h3 class="text-xl font-bold text-gray-800 mb-6">🏀 Add New Game</h3>
                    <form id="gameForm" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Date</label>
                                <input type="date" id="gameDate" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                            </div>
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Opponent</label>
                                <input type="text" id="opponent" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" placeholder="Team name" required>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Points</label>
                                <input type="number" id="points" min="0" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                            </div>
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Rebounds</label>
                                <input type="number" id="rebounds" min="0" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                            </div>
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Assists</label>
                                <input type="number" id="assists" min="0" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                            </div>
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Steals</label>
                                <input type="number" id="steals" min="0" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                            </div>
                        </div>

                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">Game Score (Win/Loss)</label>
                                <select id="gameResult" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                                    <option value="">Select result</option>
                                    <option value="win">Win 🏆</option>
                                    <option value="loss">Loss 😤</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-gray-700 font-medium mb-2">How did you feel?</label>
                                <select id="feeling" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" required>
                                    <option value="">Select feeling</option>
                                    <option value="😄">😄 Amazing</option>
                                    <option value="😊">😊 Great</option>
                                    <option value="🙂">🙂 Good</option>
                                    <option value="😐">😐 Okay</option>
                                    <option value="😔">😔 Not great</option>
                                </select>
                            </div>
                        </div>

                        <div>
                            <label class="block text-gray-700 font-medium mb-2">Game Notes</label>
                            <textarea id="notes" rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" placeholder="How did the game go? What did you learn?"></textarea>
                        </div>

                        <button type="submit" class="w-full basketball-bg text-white py-4 rounded-lg font-semibold text-lg hover:opacity-90 transition-all">
                            🏀 Add Game Stats
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- Schedule Edit Modal -->
    <div id="scheduleModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-xl p-6 max-w-md w-full mx-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">📅 Edit Schedule</h3>
            <div class="mb-4">
                <label class="block text-gray-700 font-medium mb-2">Day <span id="modalDayNumber"></span></label>
                <select id="activitySelect" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent">
                    <option value="">No activity</option>
                    <option value="practice">🏀 Practice</option>
                    <option value="game">🏆 Game</option>
                    <option value="training">💪 Training</option>
                    <option value="scrimmage">⚡ Scrimmage</option>
                    <option value="rest">😴 Rest Day</option>
                </select>
            </div>
            <div class="mb-6">
                <label class="block text-gray-700 font-medium mb-2">Time (optional)</label>
                <input type="time" id="activityTime" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent">
            </div>
            <div class="flex space-x-3">
                <button onclick="saveScheduleDay()" class="flex-1 basketball-bg text-white py-3 rounded-lg font-semibold hover:opacity-90 transition-all">
                    Save
                </button>
                <button onclick="closeScheduleModal()" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 rounded-lg font-semibold transition-all">
                    Cancel
                </button>
            </div>
        </div>
    </div>

    <script>
        // Game data storage
        let games = JSON.parse(localStorage.getItem('gamelogGames')) || [];
        let schedule = JSON.parse(localStorage.getItem('gamelogSchedule')) || {};
        let isLoggedIn = false;
        let currentEditingDay = null;

        // Achievement definitions
        const achievementsList = [
            { id: 'first_game', name: 'First Game', description: 'Play your first game', emoji: '🎯', condition: () => games.length >= 1 },
            { id: 'scorer', name: 'Scorer', description: 'Score 20+ points in a game', emoji: '🔥', condition: () => games.some(g => g.points >= 20) },
            { id: 'rebounder', name: 'Rebounder', description: 'Get 10+ rebounds in a game', emoji: '🤾', condition: () => games.some(g => g.rebounds >= 10) },
            { id: 'playmaker', name: 'Playmaker', description: 'Get 8+ assists in a game', emoji: '🎯', condition: () => games.some(g => g.assists >= 8) },
            { id: 'streak', name: 'Win Streak', description: 'Win 3 games in a row', emoji: '🔥', condition: () => checkWinStreak() },
            { id: 'consistent', name: 'Consistent', description: 'Play 10 games', emoji: '💪', condition: () => games.length >= 10 },
            { id: 'double_double', name: 'Double-Double', description: 'Get 10+ in two stats in one game', emoji: '⭐', condition: () => checkDoubleDouble() }
        ];

        // Initialize the app
        function init() {
            showPage('home');
            updateStats();
            updateChart();
            updateRecentGames();
            updateAchievements();
            updateHistoryStats();
            updateGamesList();
            updateScheduleDisplay();
            
            // Set today's date as default
            document.getElementById('gameDate').valueAsDate = new Date();
        }

        // Page navigation
        function showPage(page) {
            document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
            document.getElementById(page + 'Page').classList.remove('hidden');
            
            if (page === 'admin' && !isLoggedIn) {
                document.getElementById('loginForm').classList.remove('hidden');
                document.getElementById('adminPanel').classList.add('hidden');
            }
        }

        // Admin login
        function login() {
            const password = document.getElementById('adminPassword').value;
            if (password === 'L8sSa67') {
                isLoggedIn = true;
                document.getElementById('loginForm').classList.add('hidden');
                document.getElementById('adminPanel').classList.remove('hidden');
                document.getElementById('loginError').classList.add('hidden');
                document.getElementById('adminPassword').value = '';
            } else {
                document.getElementById('loginError').classList.remove('hidden');
            }
        }

        function logout() {
            isLoggedIn = false;
            document.getElementById('loginForm').classList.remove('hidden');
            document.getElementById('adminPanel').classList.add('hidden');
        }

        // Handle form submission
        document.getElementById('gameForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const gameData = {
                id: Date.now(),
                date: document.getElementById('gameDate').value,
                opponent: document.getElementById('opponent').value,
                points: parseInt(document.getElementById('points').value),
                rebounds: parseInt(document.getElementById('rebounds').value),
                assists: parseInt(document.getElementById('assists').value),
                steals: parseInt(document.getElementById('steals').value),
                result: document.getElementById('gameResult').value,
                feeling: document.getElementById('feeling').value,
                notes: document.getElementById('notes').value
            };

            games.push(gameData);
            localStorage.setItem('gamelogGames', JSON.stringify(games));
            
            // Reset form
            document.getElementById('gameForm').reset();
            document.getElementById('gameDate').valueAsDate = new Date();
            
            // Update displays
            updateStats();
            updateChart();
            updateRecentGames();
            updateAchievements();
            updateHistoryStats();
            updateGamesList();
            
            // Show success message
            alert('🏀 Game stats added successfully!');
        });

        // Update overall stats
        function updateStats() {
            const totalPoints = games.reduce((sum, game) => sum + game.points, 0);
            const totalRebounds = games.reduce((sum, game) => sum + game.rebounds, 0);
            const totalAssists = games.reduce((sum, game) => sum + game.assists, 0);
            const totalSteals = games.reduce((sum, game) => sum + game.steals, 0);

            document.getElementById('totalPoints').textContent = totalPoints;
            document.getElementById('totalRebounds').textContent = totalRebounds;
            document.getElementById('totalAssists').textContent = totalAssists;
            document.getElementById('totalSteals').textContent = totalSteals;
            document.getElementById('totalGames').textContent = games.length;
        }

        // Update progress chart
        function updateChart() {
            const ctx = document.getElementById('progressChart').getContext('2d');
            
            // Clear any existing chart
            Chart.getChart(ctx)?.destroy();
            
            // Get last 10 games for chart
            const recentGames = games.slice(-10);
            const labels = recentGames.map(game => new Date(game.date).toLocaleDateString());
            const pointsData = recentGames.map(game => game.points);

            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: labels,
                    datasets: [{
                        label: 'Points per Game',
                        data: pointsData,
                        borderColor: '#ff6b35',
                        backgroundColor: 'rgba(255, 107, 53, 0.1)',
                        borderWidth: 3,
                        fill: true,
                        tension: 0.4
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                color: 'rgba(0,0,0,0.1)'
                            }
                        },
                        x: {
                            grid: {
                                color: 'rgba(0,0,0,0.1)'
                            }
                        }
                    }
                }
            });
        }

        // Update recent games display
        function updateRecentGames() {
            const container = document.getElementById('recentGames');
            const recentGames = games.slice(-5).reverse();

            if (recentGames.length === 0) {
                container.innerHTML = '<div class="text-gray-500 text-center py-8">No games recorded yet! Add your first game in the Admin panel.</div>';
                return;
            }

            container.innerHTML = recentGames.map(game => `
                <div class="flex items-center justify-between p-4 bg-gray-50 rounded-lg">
                    <div class="flex items-center space-x-3">
                        <div class="text-2xl">${game.feeling}</div>
                        <div>
                            <div class="font-semibold text-gray-800">vs ${game.opponent}</div>
                            <div class="text-sm text-gray-600">${new Date(game.date).toLocaleDateString()}</div>
                        </div>
                    </div>
                    <div class="text-right">
                        <div class="font-bold text-orange-600">${game.points} pts</div>
                        <div class="text-sm text-gray-600">${game.rebounds}R ${game.assists}A ${game.steals}S</div>
                    </div>
                </div>
            `).join('');
        }

        
        function updateAchievements() {
            const container = document.getElementById('achievements');
            
            container.innerHTML = achievementsList.map(achievement => {
                const unlocked = achievement.condition();
                return `
                    <div class="achievement-card p-4 rounded-lg border-2 ${unlocked ? 'bg-yellow-50 border-yellow-300 achievement-glow' : 'bg-gray-50 border-gray-200'} text-center">
                        <div class="text-3xl mb-2 ${unlocked ? '' : 'grayscale opacity-50'}">${achievement.emoji}</div>
                        <div class="font-bold text-gray-800 mb-1">${achievement.name}</div>
                        <div class="text-sm text-gray-600">${achievement.description}</div>
                        ${unlocked ? '<div class="text-xs text-yellow-600 font-semibold mt-2">UNLOCKED!</div>' : '<div class="text-xs text-gray-400 mt-2">Locked</div>'}
                    </div>
                `;
            }).join('');
        }

        // Achievement condition helpers
        function checkWinStreak() {
            if (games.length < 3) return false;
            const lastThree = games.slice(-3);
            return lastThree.every(game => game.result === 'win');
        }

        function checkDoubleDouble() {
            return games.some(game => {
                const stats = [game.points, game.rebounds, game.assists, game.steals];
                return stats.filter(stat => stat >= 10).length >= 2;
            });
        }

        // Update history page stats
        function updateHistoryStats() {
            const wins = games.filter(game => game.result === 'win').length;
            const losses = games.filter(game => game.result === 'loss').length;
            const avgPoints = games.length > 0 ? Math.round(games.reduce((sum, game) => sum + game.points, 0) / games.length) : 0;
            const bestGame = games.length > 0 ? Math.max(...games.map(game => game.points)) : 0;

            document.getElementById('totalWins').textContent = wins;
            document.getElementById('totalLosses').textContent = losses;
            document.getElementById('avgPoints').textContent = avgPoints;
            document.getElementById('bestGame').textContent = bestGame;
        }

        // Update games list
        function updateGamesList() {
            const container = document.getElementById('gamesList');
            
            if (games.length === 0) {
                container.innerHTML = '<div class="text-gray-500 text-center py-12">No games recorded yet! Add your first game in the Admin panel.</div>';
                return;
            }

            // Sort games by date (newest first) by default
            const sortedGames = [...games].sort((a, b) => new Date(b.date) - new Date(a.date));

            container.innerHTML = sortedGames.map(game => `
                <div class="game-card bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-all">
                    <div class="flex flex-col md:flex-row md:items-center justify-between">
                        <div class="flex items-center space-x-4 mb-4 md:mb-0">
                            <div class="text-4xl">${game.feeling}</div>
                            <div>
                                <div class="flex items-center space-x-2">
                                    <h4 class="font-bold text-lg text-gray-800">vs ${game.opponent}</h4>
                                    <span class="px-2 py-1 rounded-full text-sm font-semibold ${game.result === 'win' ? 'bg-green-100 text-green-600' : 'bg-red-100 text-red-600'}">
                                        ${game.result === 'win' ? '🏆 Win' : '😤 Loss'}
                                    </span>
                                </div>
                                <div class="text-gray-600">${new Date(game.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</div>
                            </div>
                        </div>
                        
                        <div class="grid grid-cols-4 gap-4 text-center">
                            <div>
                                <div class="text-2xl font-bold text-orange-600">${game.points}</div>
                                <div class="text-xs text-gray-500">Points</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-blue-600">${game.rebounds}</div>
                                <div class="text-xs text-gray-500">Rebounds</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-green-600">${game.assists}</div>
                                <div class="text-xs text-gray-500">Assists</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-purple-600">${game.steals}</div>
                                <div class="text-xs text-gray-500">Steals</div>
                            </div>
                        </div>
                    </div>
                    
                    ${game.notes ? `
                        <div class="mt-4 pt-4 border-t border-gray-100">
                            <div class="text-sm text-gray-600">
                                <strong>Notes:</strong> ${game.notes}
                            </div>
                        </div>
                    ` : ''}
                    
                    <div class="mt-4 flex justify-end">
                        <button onclick="deleteGame(${game.id})" class="text-red-500 hover:text-red-700 text-sm font-medium">
                            🗑️ Delete Game
                        </button>
                    </div>
                </div>
            `).join('');
        }

        // Sort games function
        function sortGames(sortBy) {
            const container = document.getElementById('gamesList');
            let sortedGames;

            if (sortBy === 'date') {
                sortedGames = [...games].sort((a, b) => new Date(b.date) - new Date(a.date));
            } else if (sortBy === 'points') {
                sortedGames = [...games].sort((a, b) => b.points - a.points);
            }

            container.innerHTML = sortedGames.map(game => `
                <div class="game-card bg-white border border-gray-200 rounded-lg p-6 hover:shadow-lg transition-all">
                    <div class="flex flex-col md:flex-row md:items-center justify-between">
                        <div class="flex items-center space-x-4 mb-4 md:mb-0">
                            <div class="text-4xl">${game.feeling}</div>
                            <div>
                                <div class="flex items-center space-x-2">
                                    <h4 class="font-bold text-lg text-gray-800">vs ${game.opponent}</h4>
                                    <span class="px-2 py-1 rounded-full text-sm font-semibold ${game.result === 'win' ? 'bg-green-100 text-green-600' : 'bg-red-100 text-red-600'}">
                                        ${game.result === 'win' ? '🏆 Win' : '😤 Loss'}
                                    </span>
                                </div>
                                <div class="text-gray-600">${new Date(game.date).toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</div>
                            </div>
                        </div>
                        
                        <div class="grid grid-cols-4 gap-4 text-center">
                            <div>
                                <div class="text-2xl font-bold text-orange-600">${game.points}</div>
                                <div class="text-xs text-gray-500">Points</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-blue-600">${game.rebounds}</div>
                                <div class="text-xs text-gray-500">Rebounds</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-green-600">${game.assists}</div>
                                <div class="text-xs text-gray-500">Assists</div>
                            </div>
                            <div>
                                <div class="text-2xl font-bold text-purple-600">${game.steals}</div>
                                <div class="text-xs text-gray-500">Steals</div>
                            </div>
                        </div>
                    </div>
                    
                    ${game.notes ? `
                        <div class="mt-4 pt-4 border-t border-gray-100">
                            <div class="text-sm text-gray-600">
                                <strong>Notes:</strong> ${game.notes}
                            </div>
                        </div>
                    ` : ''}
                    
                    <div class="mt-4 flex justify-end">
                        <button onclick="deleteGame(${game.id})" class="text-red-500 hover:text-red-700 text-sm font-medium">
                            🗑️ Delete Game
                        </button>
                    </div>
                </div>
            `).join('');
        }

     
        function deleteGame(gameId) {
            if (confirm('Are you sure you want to delete this game? This cannot be undone.')) {
                games = games.filter(game => game.id !== gameId);
                localStorage.setItem('gamelogGames', JSON.stringify(games));
                
                // Update all displays
                updateStats();
                updateChart();
                updateRecentGames();
                updateAchievements();
                updateHistoryStats();
                updateGamesList();
            }
        }

        
        function updateScheduleDisplay() {
            for (let i = 0; i < 7; i++) {
                const dayElement = document.getElementById(`day-${i}`);
                const dayData = schedule[i];
                
                if (dayData && dayData.activity) {
                    const activityInfo = getActivityInfo(dayData.activity);
                    dayElement.className = `schedule-day cursor-pointer rounded-lg p-3 text-center hover:shadow-md transition-all ${activityInfo.bgColor}`;
                    
                    const activityDiv = dayElement.querySelector('.day-activity');
                    let displayText = activityInfo.text;
                    if (dayData.time) {
                        displayText += `<br><span class="text-xs opacity-75">${formatTime(dayData.time)}</span>`;
                    }
                    activityDiv.innerHTML = displayText;
                } else {
                    dayElement.className = 'schedule-day cursor-pointer bg-gray-100 rounded-lg p-3 text-center hover:shadow-md transition-all';
                    dayElement.querySelector('.day-activity').innerHTML = '';
                }
            }
        }

        function getActivityInfo(activity) {
            const activities = {
                'practice': { text: '🏀 Practice', bgColor: 'bg-orange-100', textColor: 'text-orange-600' },
                'game': { text: '🏆 Game', bgColor: 'bg-blue-100', textColor: 'text-blue-600' },
                'training': { text: '💪 Training', bgColor: 'bg-green-100', textColor: 'text-green-600' },
                'scrimmage': { text: '⚡ Scrimmage', bgColor: 'bg-purple-100', textColor: 'text-purple-600' },
                'rest': { text: '😴 Rest Day', bgColor: 'bg-gray-100', textColor: 'text-gray-600' }
            };
            return activities[activity] || { text: '', bgColor: 'bg-gray-100', textColor: 'text-gray-600' };
        }

        function formatTime(time) {
            const [hours, minutes] = time.split(':');
            const hour = parseInt(hours);
            const ampm = hour >= 12 ? 'PM' : 'AM';
            const displayHour = hour % 12 || 12;
            return `${displayHour}:${minutes} ${ampm}`;
        }

        function editScheduleDay(dayIndex) {
            currentEditingDay = dayIndex;
            const dayData = schedule[dayIndex] || {};
            
            document.getElementById('modalDayNumber').textContent = dayIndex + 1;
            document.getElementById('activitySelect').value = dayData.activity || '';
            document.getElementById('activityTime').value = dayData.time || '';
            
            document.getElementById('scheduleModal').classList.remove('hidden');
        }

        function saveScheduleDay() {
            const activity = document.getElementById('activitySelect').value;
            const time = document.getElementById('activityTime').value;
            
            if (activity) {
                schedule[currentEditingDay] = { activity, time };
            } else {
                delete schedule[currentEditingDay];
            }
            
            localStorage.setItem('gamelogSchedule', JSON.stringify(schedule));
            updateScheduleDisplay();
            closeScheduleModal();
        }

        function closeScheduleModal() {
            document.getElementById('scheduleModal').classList.add('hidden');
            currentEditingDay = null;
        }

        // Close modal when clicking outside
        document.getElementById('scheduleModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeScheduleModal();
            }
        });

        // Initialize app when page loads
        window.addEventListener('load', init);
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97ba4068c5d297fd',t:'MTc1NzI5MDUyOC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
