<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>建設時間短縮計算ツール</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        .container { 
            display: inline-block; 
            text-align: left; 
            border: 2px solid #333; 
            padding: 20px; 
            border-radius: 10px; 
            background-color: #f9f9f9;
        }
        input { margin: 5px; padding: 8px; width: 80px; }
        button { padding: 10px; margin-top: 10px; cursor: pointer; }
        #result { margin-top: 15px; font-size: 1.2em; font-weight: bold; }
    </style>
</head>
<body>
    <h2>ホワイトアウトサバイバル 建設時間計算ツール</h2>
    <div class="container">
        <label>初期建設時間（日）: <input type="number" id="initialDays" value="0" min="0"></label><br>
        <label>初期建設時間（時間）: <input type="number" id="initialHours" value="0" min="0"></label><br>
        <label>建造速度ボーナス（%）: <input type="number" id="speedBonus" value="0" min="0"></label><br>
        <label>追加時短（%）: <input type="number" id="extraReduction" value="0" min="0"></label><br>
        <button onclick="calculateTime()">計算する</button>
        <h3 id="result"></h3>
    </div>

    <script>
        function calculateTime() {
            let initialDays = Number(document.getElementById("initialDays").value) || 0;
            let initialHours = Number(document.getElementById("initialHours").value) || 0;
            let speedBonus = Number(document.getElementById("speedBonus").value) || 0;
            let extraReduction = Number(document.getElementById("extraReduction").value) || 0;

            let initialTimeInHours = (initialDays * 24) + initialHours;
            let speedMultiplier = 1 + (speedBonus / 100); // 例: 82.4% → 1.824
            let reducedTimeInHours = initialTimeInHours / speedMultiplier; // 建造速度ボーナスで時間を割る
            
            let extraMultiplier = 1 - (extraReduction / 100);
            if (extraMultiplier < 0) extraMultiplier = 0;
            reducedTimeInHours *= extraMultiplier; // 追加時短を適用
            
            let finalDays = Math.floor(reducedTimeInHours / 24);
            let finalHours = Math.round(reducedTimeInHours % 24);

            document.getElementById("result").innerText = `短縮後の建設時間: ${finalDays}日 ${finalHours}時間`;
        }
    </script>
</body>
</html>
