# Definuj cestu k pracovní ploše
$desktopPath = [Environment]::GetFolderPath('Desktop')

# Definuj cestu k souboru index.html na pracovní ploše
$indexHtmlPath = "$desktopPath\index.html"

# Definuj obsah souboru index.html s efekty padajících koulí, stylizovaným pozadím a vyhledáváním URL
$htmlContent = @"
<!DOCTYPE html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background: linear-gradient(135deg, #000000, #4B0082);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            font-family: Arial, sans-serif;
        }
        .container {
            text-align: center;
            z-index: 10;
        }
        .ball {
            position: absolute;
            background-color: white;
            border-radius: 50%;
            width: 10px;
            height: 10px;
            animation: fall infinite linear;
        }
        @keyframes fall {
            0% {
                top: -10px;
                opacity: 1;
            }
            100% {
                top: 100vh;
                opacity: 0;
            }
        }
        input[type="text"] {
            padding: 10px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            width: 300px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            background-color: #4B0082;
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <input type="text" id="url" placeholder="Zadejte URL">
        <button onclick="searchUrl()">Vyhledat</button>
    </div>
    <script>
        function createBall() {
            const ball = document.createElement("div");
            ball.classList.add("ball");
            ball.style.left = Math.random() * 100 + "vw";
            ball.style.animationDuration = Math.random() * 2 + 3 + "s";
            document.body.appendChild(ball);
            setTimeout(() => {
                ball.remove();
            }, 5000);
        }
        setInterval(createBall, 100);

        function searchUrl() {
            const url = document.getElementById("url").value;
            if (url) {
                window.location.href = url;
            }
        }
    </script>
</body>
</html>
"@

# Vytvoř soubor index.html a zapiš do něj obsah
Set-Content -Path $indexHtmlPath -Value $htmlContent

Write-Output "index.html byl vytvořen na vaší pracovní ploše."
``` ▋
