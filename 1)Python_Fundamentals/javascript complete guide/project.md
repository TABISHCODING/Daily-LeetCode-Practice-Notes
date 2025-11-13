# 🎯 **JavaScript Practice Projects**

**Hands-on Practice | Hinglish Friendly | Build Real Projects**

---

## **Project 1: DOM Mini-Project - Todo List**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Todo List (Hinglish)</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
        }
        .todo-item {
            padding: 10px;
            margin: 5px 0;
            background: #f0f0f0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
        }
        .completed {
            text-decoration: line-through;
            opacity: 0.6;
        }
    </style>
</head>
<body>
    <h1>📝 Todo List (Hinglish mein)</h1>
    <input type="text" id="todoInput" placeholder="Kya karna hai?">
    <button id="addBtn">Add Karo</button>
    <div id="todoList"></div>

    <script>
        // DOM elements select karo
        const input = document.getElementById('todoInput');
        const addBtn = document.getElementById('addBtn');
        const todoList = document.getElementById('todoList');

        // Todos array
        let todos = [];

        // Add todo function
        function addTodo() {
            const text = input.value.trim();
            if (!text) {
                alert('Kuch toh likho!');
                return;
            }

            const todo = {
                id: Date.now(),
                text: text,
                completed: false
            };

            todos.push(todo);
            input.value = '';
            renderTodos();
        }

        // Toggle todo
        function toggleTodo(id) {
            const todo = todos.find(t => t.id === id);
            if (todo) {
                todo.completed = !todo.completed;
                renderTodos();
            }
        }

        // Delete todo
        function deleteTodo(id) {
            todos = todos.filter(t => t.id !== id);
            renderTodos();
        }

        // Render todos
        function renderTodos() {
            todoList.innerHTML = '';
            
            todos.forEach(todo => {
                const div = document.createElement('div');
                div.className = `todo-item ${todo.completed ? 'completed' : ''}`;
                div.innerHTML = `
                    <span onclick="toggleTodo(${todo.id})">${todo.text}</span>
                    <button onclick="deleteTodo(${todo.id})">Delete</button>
                `;
                todoList.appendChild(div);
            });
        }

        // Event listeners
        addBtn.addEventListener('click', addTodo);
        input.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTodo();
        });

        // Hinglish: Yeh simple todo list hai - add, toggle, delete kar sakte ho
    </script>
</body>
</html>
```

---

## **Project 2: Fetch API - Weather App**

```javascript
// Weather App (Hinglish comments)

const API_KEY = 'your_api_key_here'; // OpenWeatherMap se API key lo
const searchBtn = document.getElementById('searchBtn');
const cityInput = document.getElementById('cityInput');
const weatherDiv = document.getElementById('weather');

// Weather fetch karo
async function getWeather(city) {
    try {
        weatherDiv.innerHTML = '<p>Loading... (Thoda wait karo)</p>';
        
        const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric`;
        
        const response = await fetch(url);
        
        if (!response.ok) {
            throw new Error('City nahi mili!');
        }
        
        const data = await response.json();
        
        // Weather display karo
        displayWeather(data);
        
    } catch (error) {
        weatherDiv.innerHTML = `<p style="color: red;">Error: ${error.message}</p>`;
    }
}

// Weather display karne ka function
function displayWeather(data) {
    const { name, main, weather } = data;
    
    const html = `
        <div class="weather-card">
            <h2>${name}</h2>
            <p class="temp">${Math.round(main.temp)}°C</p>
            <p>${weather[0].description}</p>
            <p>Feels like: ${Math.round(main.feels_like)}°C</p>
            <p>Humidity: ${main.humidity}%</p>
        </div>
    `;
    
    weatherDiv.innerHTML = html;
}

// Event listener
searchBtn.addEventListener('click', () => {
    const city = cityInput.value.trim();
    if (city) {
        getWeather(city);
    } else {
        alert('City naam dalo!');
    }
});

// Hinglish: Async/await aur Fetch API ka use kiya hai
```

---

## **Project 3: Form Validation**

```javascript
// Form Validation (Hinglish)

const form = document.getElementById('registrationForm');
const usernameInput = document.getElementById('username');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');
const confirmPasswordInput = document.getElementById('confirmPassword');

// Validation functions
function validateUsername(username) {
    if (username.length < 3) {
        return 'Username 3 characters se zyada hona chahiye!';
    }
    return null; // Valid hai
}

function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(email)) {
        return 'Valid email dalo!';
    }
    return null;
}

function validatePassword(password) {
    if (password.length < 6) {
        return 'Password 6 characters se zyada hona chahiye!';
    }
    if (!/[A-Z]/.test(password)) {
        return 'Password mein ek capital letter hona chahiye!';
    }
    if (!/[0-9]/.test(password)) {
        return 'Password mein ek number hona chahiye!';
    }
    return null;
}

function validateConfirmPassword(password, confirmPassword) {
    if (password !== confirmPassword) {
        return 'Passwords match nahi kar rahe!';
    }
    return null;
}

// Show error function
function showError(input, message) {
    const formGroup = input.parentElement;
    const errorDiv = formGroup.querySelector('.error-message') || document.createElement('div');
    errorDiv.className = 'error-message';
    errorDiv.textContent = message;
    errorDiv.style.color = 'red';
    errorDiv.style.fontSize = '12px';
    
    if (!formGroup.querySelector('.error-message')) {
        formGroup.appendChild(errorDiv);
    }
    
    input.style.borderColor = 'red';
}

// Clear error function
function clearError(input) {
    const formGroup = input.parentElement;
    const errorDiv = formGroup.querySelector('.error-message');
    if (errorDiv) {
        errorDiv.remove();
    }
    input.style.borderColor = '';
}

// Real-time validation (Hinglish: Type karte hi check ho jayega)
usernameInput.addEventListener('input', () => {
    const error = validateUsername(usernameInput.value);
    if (error) {
        showError(usernameInput, error);
    } else {
        clearError(usernameInput);
    }
});

emailInput.addEventListener('input', () => {
    const error = validateEmail(emailInput.value);
    if (error) {
        showError(emailInput, error);
    } else {
        clearError(emailInput);
    }
});

passwordInput.addEventListener('input', () => {
    const error = validatePassword(passwordInput.value);
    if (error) {
        showError(passwordInput, error);
    } else {
        clearError(passwordInput);
    }
});

confirmPasswordInput.addEventListener('input', () => {
    const error = validateConfirmPassword(passwordInput.value, confirmPasswordInput.value);
    if (error) {
        showError(confirmPasswordInput, error);
    } else {
        clearError(confirmPasswordInput);
    }
});

// Form submit
form.addEventListener('submit', (e) => {
    e.preventDefault();
    
    // Sabhi validations check karo
    const usernameError = validateUsername(usernameInput.value);
    const emailError = validateEmail(emailInput.value);
    const passwordError = validatePassword(passwordInput.value);
    const confirmPasswordError = validateConfirmPassword(passwordInput.value, confirmPasswordInput.value);
    
    // Agar koi error hai toh submit mat karo
    if (usernameError || emailError || passwordError || confirmPasswordError) {
        alert('Form mein errors hain! Pehle unhe fix karo.');
        return;
    }
    
    // Submit successful
    alert('Registration successful! 🎉');
    form.reset();
});

// Hinglish: Real-time validation implemented hai - user ko turant feedback milega
```

---

## **Project 4: Debouncing Search**

```javascript
// Debounced Search (Hinglish)

const searchInput = document.getElementById('searchInput');
const resultsDiv = document.getElementById('results');

// Debounce function (Interview important!)
function debounce(func, delay) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => func.apply(this, args), delay);
    };
}

// Search function
async function search(query) {
    if (!query.trim()) {
        resultsDiv.innerHTML = '';
        return;
    }
    
    resultsDiv.innerHTML = '<p>Searching... (API call ho rahi hai)</p>';
    
    try {
        // API call (example: GitHub users)
        const response = await fetch(`https://api.github.com/search/users?q=${query}`);
        const data = await response.json();
        
        // Results display karo
        displayResults(data.items);
        
    } catch (error) {
        resultsDiv.innerHTML = '<p style="color: red;">Error aa gaya!</p>';
    }
}

// Display results
function displayResults(users) {
    if (users.length === 0) {
        resultsDiv.innerHTML = '<p>Koi result nahi mila!</p>';
        return;
    }
    
    const html = users.slice(0, 10).map(user => `
        <div style="padding: 10px; border-bottom: 1px solid #ddd;">
            <img src="${user.avatar_url}" width="50" style="border-radius: 50%;">
            <strong>${user.login}</strong>
        </div>
    `).join('');
    
    resultsDiv.innerHTML = html;
}

// Debounced search (300ms delay)
const debouncedSearch = debounce(search, 300);

// Event listener
searchInput.addEventListener('input', (e) => {
    debouncedSearch(e.target.value);
});

// Hinglish: Har keystroke pe API call nahi hogi, 300ms wait karega
// Yeh performance optimization hai - interview mein useful!
```

---

## **Project 5: Promise Practice - Sequential API Calls**

```javascript
// Sequential API Calls (Hinglish)

// Mock API functions (simulate network delay)
function fetchUser(userId) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({ id: userId, name: 'Rahul Kumar' });
        }, 1000);
    });
}

function fetchPosts(userId) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve([
                { id: 1, title: 'Post 1', userId },
                { id: 2, title: 'Post 2', userId }
            ]);
        }, 1000);
    });
}

function fetchComments(postId) {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve([
                { id: 1, text: 'Great post!', postId },
                { id: 2, text: 'Nice!', postId }
            ]);
        }, 1000);
    });
}

// Approach 1: Promise Chaining (Hinglish: Ek ke baad ek)
console.log('--- Promise Chaining Start ---');
fetchUser(1)
    .then(user => {
        console.log('User mila:', user);
        return fetchPosts(user.id);
    })
    .then(posts => {
        console.log('Posts mile:', posts);
        return fetchComments(posts[0].id);
    })
    .then(comments => {
        console.log('Comments mile:', comments);
    })
    .catch(error => {
        console.log('Error:', error);
    });

// Approach 2: Async/Await (Modern, clean)
async function getData() {
    try {
        console.log('--- Async/Await Start ---');
        
        const user = await fetchUser(1);
        console.log('User mila:', user);
        
        const posts = await fetchPosts(user.id);
        console.log('Posts mile:', posts);
        
        const comments = await fetchComments(posts[0].id);
        console.log('Comments mile:', comments);
        
    } catch (error) {
        console.log('Error:', error);
    }
}

getData();

// Approach 3: Parallel Execution (Jab dependent nahi ho)
async function getDataParallel() {
    try {
        console.log('--- Parallel Execution Start ---');
        
        const [user1, user2, user3] = await Promise.all([
            fetchUser(1),
            fetchUser(2),
            fetchUser(3)
        ]);
        
        console.log('Sab users ek saath mile:', user1, user2, user3);
        
    } catch (error) {
        console.log('Error:', error);
    }
}

getDataParallel();

// Hinglish: Async operations handle karne ke 3 tarike dikhaye
// Interview mein bahut poocha jata hai!
```

---

## **💡 Practice Tips (Hinglish Mein)**

1. **Daily 1 hour practice karo** - Consistency important hai
2. **Projects ko modify karo** - Apne ideas add karo
3. **Console.log() use karo** - Debugging ke liye
4. **Errors ko samjho** - Error messages padhna seekho
5. **MDN documentation padhte raho** - Reference ke liye best hai
6. **LeetCode/HackerRank pe practice karo** - Algorithms ke liye
7. **GitHub pe projects upload karo** - Portfolio banao
8. **Code review lo** - Dusron se feedback maango

---

**🎯 Next Steps:**

1. In projects ko implement karo
2. Features add karo (like localStorage, better UI)
3. Apne projects banao
4. Portfolio website mein add karo
5. GitHub pe share karo

**Happy Coding! Practice karte raho! 💪🚀**

