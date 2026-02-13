# The Epsilon-Delta Game v4.2

An interactive educational game that transforms the epsilon-delta definition of limits into an engaging strategic challenge.

## 🎮 Game Features

- **4 Progressive Levels**: Tutorial, Linear, Square Root, Quadratic, and Trigonometric functions
- **Practice Mode**: Free exploration without scoring pressure
- **Interactive Visualization**: Real-time epsilon-delta proof visualization
- **Educational Content**: Comprehensive learning materials and hints
- **Audio System**: Background music and sound effects with volume control
- **Scoring System**: Star-based progression with hint penalties

## 📦 What's New in v4.2

### Fixed Issues from v4.1
- ✅ **Hash-Based Routing**: Fixed 404 errors on GitHub Pages by switching to hash routing
- ✅ **URL Structure**: URLs now use `#/` format (e.g., `https://pyaim.github.io/epsilon-delta/#/levels`)
- ✅ **Page Refresh**: No more 404 errors when refreshing pages
- ✅ **GitHub Pages Support**: Perfect compatibility with subdirectory deployment

### Previous Fixes (v4.1)
- ✅ **Audio Interference**: Removed button click sounds that interrupted background music
- ✅ **Sound Effect Volume**: Reduced from 0.3 to 0.15 for better music coexistence
- ✅ **Clean Build**: Removed all Manus-specific dependencies and metadata

### Level 4: Trigonometric Master
- Function: **sin(x)/x** approaching 1 as x → 0
- Beautiful sinc function visualization
- Progressive epsilon challenges: 1.0 → 0.5 → 0.1
- Teaches the famous limit used in calculus and signal processing

## 🚀 Deployment Options

### Option 1: GitHub Pages (Recommended)

**Pros:**
- ✅ Free hosting with HTTPS
- ✅ Custom domain support
- ✅ Automatic deployments via Git
- ✅ Global CDN distribution
- ✅ Zero configuration needed

**Steps:**
```bash
# 1. Initialize Git repository
git init
git add .
git commit -m "Initial commit: Epsilon-Delta Game v4.2"

# 2. Create GitHub repository at https://github.com/new
# Repository name: epsilon-delta
# Visibility: Public

# 3. Push to GitHub
git remote add origin https://github.com/YOUR_USERNAME/epsilon-delta.git
git branch -M main
git push -u origin main

# 4. Enable GitHub Pages
# Go to: Settings → Pages
# Source: Deploy from a branch
# Branch: main / / (root)
# Save

# 5. Access your site (wait 1-2 minutes)
# https://YOUR_USERNAME.github.io/epsilon-delta/#/
```

### Option 2: Self-Hosted (nginx)

**Pros:**
- ✅ Full control over infrastructure
- ✅ No external dependencies
- ✅ Custom SSL certificates
- ✅ Integration with existing homelab

**nginx Configuration:**
```nginx
server {
    listen 80;
    server_name epsilon-delta.yourdomain.com;
    
    root /var/www/epsilon-delta;
    index index.html;
    
    # SPA routing - serve index.html for all routes
    location / {
        try_files $uri $uri/ /index.html;
    }
    
    # Cache static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

### Option 3: Kubernetes (Homelab)

**Pros:**
- ✅ Scalable and resilient
- ✅ GitOps with ArgoCD
- ✅ Monitoring with Prometheus/Grafana
- ✅ Automated deployments

**Deployment Manifest:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: epsilon-delta-game
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: epsilon-delta-game
  template:
    metadata:
      labels:
        app: epsilon-delta-game
    spec:
      containers:
      - name: nginx
        image: nginx:alpine
        ports:
        - containerPort: 80
        volumeMounts:
        - name: app-files
          mountPath: /usr/share/nginx/html
      volumes:
      - name: app-files
        configMap:
          name: epsilon-delta-files
---
apiVersion: v1
kind: Service
metadata:
  name: epsilon-delta-game
spec:
  selector:
    app: epsilon-delta-game
  ports:
  - port: 80
    targetPort: 80
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: epsilon-delta-game
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  rules:
  - host: epsilon-delta.yourdomain.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: epsilon-delta-game
            port:
              number: 80
  tls:
  - hosts:
    - epsilon-delta.yourdomain.com
    secretName: epsilon-delta-tls
```

## 🏠 Homelab Deployment Recommendations

### Should You Use a Dedicated Proxmox VM?

**Use Kubernetes (Recommended):**
- ✅ You already have a K8s cluster
- ✅ ArgoCD for GitOps deployments
- ✅ Prometheus/Grafana monitoring in place
- ✅ Minimal resource overhead (static files)
- ✅ Easy rollbacks and updates

**Use Dedicated VM if:**
- ❌ You want isolation from cluster
- ❌ You need custom nginx configurations
- ❌ You're testing infrastructure changes

### Resource Requirements

**Kubernetes Pod:**
- CPU: 100m (0.1 core)
- Memory: 64Mi
- Storage: 5Mi (static files)

**Dedicated VM:**
- CPU: 1 vCore
- RAM: 512MB
- Disk: 5GB
- OS: Ubuntu 22.04 minimal

## 📁 File Structure

```
epsilon-delta-v4.2-production/
├── index.html              # Main HTML file (SPA entry point)
├── assets/                 # JavaScript, CSS, fonts, images
│   ├── index-*.js         # Main application bundle
│   ├── index-*.css        # Compiled Tailwind CSS
│   └── KaTeX_*            # Math rendering fonts
├── audio/                  # Background music (CDN URLs in code)
└── README.md              # This file
```

## 🔧 Technical Stack

- **Frontend**: React 19 + TypeScript
- **Routing**: Wouter (client-side SPA routing)
- **Styling**: Tailwind CSS 4
- **Math Rendering**: KaTeX
- **Graphing**: Recharts
- **Audio**: Web Audio API + HTML5 Audio

## 🌐 Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile)

## 📝 License

This educational game is provided as-is for learning purposes.

## 🎓 Educational Use

Perfect for:
- Calculus courses (limits and continuity)
- Self-study and exam preparation
- Interactive classroom demonstrations
- Flipped classroom assignments

## 🐛 Known Issues

None! All issues from v4.0 and v4.1 have been resolved in v4.2.

## 📞 Support

For questions or issues, please open an issue on the GitHub repository.

---

**Built with ❤️ for calculus students everywhere**
