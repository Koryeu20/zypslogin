// server.js
const express = require('express');
const app = express();
const bodyParser = require('body-parser');
const rateLimiter = require('express-rate-limit');
const compression = require('compression');
const chalk = require('chalk');
const fs = require("fs");
const path = require("path");
const axios = require("axios");

const DATA_FILE = path.join(__dirname, "data.txt");

// ---------------- MIDDLEWARE ----------------
app.use(compression({ level: 5, threshold: 0 }));
app.set('view engine', 'ejs');
app.set('trust proxy', 1);

app.use((req, res, next) => {
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept');
    console.log(`[${new Date().toLocaleString()}] ${req.method} ${req.url} - ${res.statusCode}`);
    next();
});

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.json());

app.use(rateLimiter({ windowMs: 15 * 60 * 1000, max: 500, headers: true }));

// ---------------- ROUTES ----------------

// API: return server list from data.txt
app.get("/api/servers", (req, res) => {
    fs.readFile(DATA_FILE, "utf8", (err, data) => {
        if (err) return res.status(500).json({ error: "Error reading data file" });

        const servers = data
            .split("\n")
            .map(line => line.trim())
            .filter(line => line.includes(" - "))
            .map(line => {
                const [name, port] = line.split(" - ");
                return { name: name.trim(), port: port?.trim() || "" };
            });

        res.json(servers);
    });
});

// Web UI: edit server list
app.get("/editserver", (req, res) => {
    fs.readFile(DATA_FILE, "utf8", (err, data) => {
        if (err) return res.status(500).send("Error reading data file");

        res.send(`
            <!DOCTYPE html>
            <html>
            <head>
                <title>Edit Server List</title>
                <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
            </head>
            <body class="bg-gray-900 text-white p-6">
                <div class="max-w-2xl mx-auto bg-gray-800 p-6 rounded-lg">
                    <h1 class="text-2xl mb-4 font-bold">Edit Server List</h1>
                    <form action="/editserver" method="post">
                        <textarea name="serverData" rows="20" class="w-full bg-black text-white p-2">${data}</textarea>
                        <button type="submit" class="bg-blue-600 mt-4 px-4 py-2 rounded">Save</button>
                    </form>
                </div>
            </body>
            </html>
        `);
    });
});

app.post("/editserver", (req, res) => {
    fs.writeFile(DATA_FILE, req.body.serverData, "utf8", err => {
        if (err) return res.status(500).send("Error saving data file");
        res.redirect("/editserver");
    });
});

// Dashboard login
app.all('/player/login/dashboard', (req, res) => {
    console.log("dashboard body:", req.body);
    const tData = {};

    try {
        const uData = JSON.stringify(req.body).split('"')[1].split('\\n');
        for (let i = 0; i < uData.length - 1; i++) {
            const d = uData[i].split('|');
            tData[d[0]] = d[1];
        }
    } catch (err) {
        console.log("Warning parsing body:", err.message);
    }

    res.render(path.join(__dirname, 'public/html/dashboard.ejs'), { data: tData || {} });
});

// Blocked login page
app.all('/player/growid/login/blocked', (req, res) => {
    res.send(`
        <html><body class="bg-black text-white flex items-center justify-center h-screen">
        <div class="p-6 bg-gray-800 rounded">
            <h1 class="text-3xl font-bold">LOGIN BLOCKED</h1>
            <p>Something unusual detected during login.</p>
            <a href="/player/login/dashboard" class="mt-4 inline-block bg-blue-600 px-4 py-2 rounded">Try Again</a>
        </div>
        </body></html>
    `);
});

// GrowID token check
app.all('/player/growid/checktoken', (req, res) => {
    const refreshToken = req.body.refreshToken || "none";
    res.json({
        status: "success",
        message: "Account Validated.",
        token: refreshToken,
        url: "",
        accountType: "growtopia"
    });
});

// GrowID validation
app.all('/player/growid/login/validate', (req, res) => {
    const rawToken = req.body._token || "{}";
    const tokenData = JSON.parse(rawToken);
    tokenData.tankIDName = req.body.growId;
    tokenData.tankIDPass = req.body.password;
    tokenData.type = req.body.type;
    tokenData.port = req.body.port;

    const token = Buffer.from(`_token=${JSON.stringify(tokenData)}`).toString('base64');
    console.log(`GROWID: ${tokenData.tankIDName} >> PASSWORD: ${tokenData.tankIDPass} >> MODE: ${req.body.type} >> PORT: ${req.body.port}`);

    res.json({
        status: "success",
        message: "Account Validated.",
        token: token,
        url: "",
        accountType: "growtopia"
    });
});

// Catch-all redirect for /player/*
app.all('/player/*', (req, res) => {
    res.status(301).redirect('https://api.yoruakio.tech/player/' + req.path.slice(8));
});

// ---------------- SERVER START ----------------
const PORT = 5000;
app.listen(PORT, () => console.log(`🚀 Server listening on http://localhost:${PORT}`));
