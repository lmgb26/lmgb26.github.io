<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Italian Flags</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background: white;
        }
        
        .flag {
            position: absolute;
            width: 80px;
            height: 50px;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <script>
        class Flag {
            constructor() {
                this.element = document.createElement('img');
                this.element.className = 'flag';
                this.element.src = 'data:image/svg+xml,' + encodeURIComponent(`
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 3 2">
                        <rect width="1" height="2" fill="#009246"/>
                        <rect x="1" width="1" height="2" fill="#fff"/>
                        <rect x="2" width="1" height="2" fill="#ce2b37"/>
                    </svg>
                `);
                
                this.x = Math.random() * window.innerWidth;
                this.y = Math.random() * window.innerHeight;
                this.speedX = (Math.random() - 0.5) * 4;
                this.speedY = (Math.random() - 0.5) * 4;
                
                this.element.style.left = this.x + 'px';
                this.element.style.top = this.y + 'px';
                
                document.body.appendChild(this.element);
            }
            
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                
                if (this.x <= 0 || this.x >= window.innerWidth - 80) {
                    this.speedX = -this.speedX;
                }
                if (this.y <= 0 || this.y >= window.innerHeight - 50) {
                    this.speedY = -this.speedY;
                }
                
                this.element.style.left = this.x + 'px';
                this.element.style.top = this.y + 'px';
            }
        }
        
        const flags = [];
        for (let i = 0; i < 15; i++) {
            flags.push(new Flag());
        }
        
        function animate() {
            flags.forEach(flag => flag.update());
            requestAnimationFrame(animate);
        }
        
        animate();
        
        window.addEventListener('resize', () => {
            flags.forEach(flag => {
                if (flag.x > window.innerWidth - 80) flag.x = window.innerWidth - 80;
                if (flag.y > window.innerHeight - 50) flag.y = window.innerHeight - 50;
            });
        });
    </script>
</body>
</html>
