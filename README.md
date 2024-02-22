// Step 1: Set up your project with npm and install required packages
// Run `npm init` to create a new npm project and follow the prompts
// Then, install required packages using `npm install express body-parser axios`

// Step 2: Create your main application file (e.g., app.js)
const express = require('express');
const bodyParser = require('body-parser');
const axios = require('axios');

const app = express();
const PORT = process.env.PORT || 3000
// Middleware
app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static('public')); // Serve static files (e.g., CSS, images)

// Routes
app.get('/', (req, res) => {
    res.sendFile(__dirname + '/index.html'); // Serve HTML file for user input
});

app.post('/number', (req, res) => {
    const number = req.body.number;

    // Perform basic operations or fetch trivia about the number
    const numberInfo = {
        number: number,
        isPrime: checkPrime(number),
        // Add more properties or calculations as needed
    };

    res.send(numberInfo);
});

// Helper function to check if a number is prime
function checkPrime(number) {
    if (number <= 1) return false;
    if (number <= 3) return true;
    if (number % 2 === 0 || number % 3 === 0) return false;
    let i = 5;
    while (i * i <= number) {
        if (number % i === 0 || number % (i + 2) === 0) return false;
        i += 6;
    }
    return true;
}

// Start the server
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
