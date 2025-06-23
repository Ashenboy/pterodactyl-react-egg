# 🌀 React Web App - Pterodactyl Egg

A custom [Pterodactyl Panel](https://pterodactyl.io) egg for deploying React web applications with flexible configuration options for ports, build modes, and Git integration.

---
![{E68D5765-E6AF-4280-966A-BC9827A366E0}](https://github.com/user-attachments/assets/ced1b1fd-e97f-4b85-90db-3bc862742cbf)

## 🚀 Features

- 🔄 Dual Build Modes: Development (hot reload) & Production (optimized build)
- 🔧 Configurable Port: Run on any port between 1024–65535
- 🌐 Git Integration: Clone React apps directly from GitHub or GitLab
- 🔁 Auto Updates: Optional Git pulls on container restart
- 📦 Serve Options: Choose between `serve` or `http-server` in production
- 📂 Manual Upload: Upload project files directly if needed
- ➕ NPM Control: Install or uninstall additional packages easily

---

## 📋 Requirements

- ✅ Pterodactyl Panel v1.0+
- 🐳 Docker support
- 📁 React project with a valid `package.json` file

---

## 🛠️ Installation

1. **Download Egg**  
   Get the `egg-react-web-app.json` from this repository.

2. **Import into Panel**  
   - Navigate to your Pterodactyl **Admin Panel**
   - Go to `Nests → Import Egg`
   - Upload the `.json` file
   - Assign it to a Nest (e.g., create a new one called "Web Apps")

---

## ⚙️ Configuration Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `GIT_ADDRESS` | URL of Git repo | — | ✅ (unless manual upload) |
| `BRANCH` | Branch to clone | — | ❌ |
| `PORT` | Port to serve app on | 3000 | ✅ |
| `BUILD_MODE` | `development` or `production` | development | ✅ |
| `SERVE_METHOD` | Serve method for production (`serve`/`http-server`) | serve | ✅ |
| `UPLOAD_MODE` | Skip git (1 = manual upload) | 0 | ❌ |
| `AUTO_UPDATE` | Pull on startup (1 = yes) | 0 | ❌ |
| `NODE_PACKAGES` | Additional npm packages | — | ❌ |
| `GIT_USER` | Git username (private repos) | — | ❌ |
| `GIT_TOKEN` | Git personal access token | — | ❌ |
| `UNINSTALL_PACKAGES` | NPM packages to remove | — | ❌ |

---

## 🔧 Build Modes

### 💻 Development Mode

- Runs `npm start`
- Hot-reloading enabled
- Accessible via `http://your-server:PORT`

### 🌍 Production Mode

- Runs `npm run build`
- Serves static files using either:
  - `serve`: `npx serve -s build -l PORT`
  - `http-server`: `npx http-server build -p PORT -a 0.0.0.0`

---

## 📁 Project Requirements

Your React repo should include:

```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  }
}
```

---

## 🔗 Usage Examples

### ✅ Public Repo (Development)
```
GIT_ADDRESS: https://github.com/username/project
BRANCH: main
PORT: 3000
BUILD_MODE: development
```

### 🔒 Private Repo (Production)
```
GIT_ADDRESS: https://github.com/user/private-app
GIT_USER: username
GIT_TOKEN: your_token_here
PORT: 8080
BUILD_MODE: production
SERVE_METHOD: serve
```

### 🖐️ Manual Upload
```
UPLOAD_MODE: 1
PORT: 3000
BUILD_MODE: production
```

---

## 🚦 Startup Detection

The egg waits for startup logs like:
- `webpack compiled`
- `Local:`
- `On Your Network:`
- `compiled successfully`
- `Serving at http`
- `Available on:`

---

## 🐳 Docker Images

- Node.js 21: `ghcr.io/parkervcp/yolks:nodejs_21`
- Node.js 20 *(Recommended)*: `ghcr.io/parkervcp/yolks:nodejs_20`
- Node.js 18: `ghcr.io/parkervcp/yolks:nodejs_18`

---

## 🔬 Advanced Usage

### Auto Environment Injection
- `HOST=0.0.0.0`
- `PORT=${PORT}`

### Custom Scripts
If you use a custom build system:
```json
{
  "scripts": {
    "start": "custom-start",
    "build": "custom-build"
  }
}
```

---

## 🐛 Troubleshooting

| Problem | Solution |
|--------|----------|
| ❌ Build fails | Ensure `package.json` is valid |
| 🔒 Repo clone fails | Check token or access permissions |
| 🚫 Port not working | Verify server port allocation |
| 📦 Missing dependencies | Add them to `NODE_PACKAGES` |

---

## 🤝 Contributing

1. Fork the repo  
2. Create a feature branch  
3. Commit and push  
4. Submit a pull request 🙌

---

## 📄 License

Distributed under the [MIT License](LICENSE).

---

## 📬 Support

- Open an issue in this repo  
- Refer to [Pterodactyl Docs](https://pterodactyl.io)  
- Join the community on Discord  

---

**Author**: ashenetugala@gmail.com  
**Version**: 1.0.0  
**Compatibility**: Pterodactyl Panel v1.0+
