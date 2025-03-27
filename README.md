<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>《鈴芽之旅》互動閱讀介面</title>
    <style>
        body {
            font-family: "Microsoft JhengHei", Arial, sans-serif;
            line-height: 1.6;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
            background-color: #f0f0f0;
        }
        #reading-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h2 {
            color: #333;
        }
        p {
            margin-bottom: 15px;
            cursor: pointer;
        }
        .annotated {
            font-weight: bold;
            cursor: pointer;
        }
        .note {
            display: none;
            background-color: #e1f5fe;
            border-left: 5px solid #03a9f4;
            padding: 10px;
            margin-top: 10px;
            margin-bottom: 10px;
        }
        #audio-controls {
            margin-bottom: 20px;
            padding: 15px;
            background-color: #e8f5e9;
            border-radius: 5px;
        }
        button {
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            border-radius: 5px;
        }
        #speed-control {
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div id="audio-controls">
        <button onclick="togglePlayPause()" id="playPauseBtn">播放</button>
        <button onclick="stopReading()">停止</button>
        <div id="speed-control">
            <label for="speed">語速：</label>
            <input type="range" id="speed" min="0.5" max="2" step="0.1" value="1" onchange="changeSpeed(this.value)">
            <span id="speed-value">1x</span>
        </div>
    </div>

    <div id="reading-container">
        <p>今年是日本311大地震（東北地方太平洋近海地震）十二週年，對於這場世界級的震災，日本仍坎坷地走在漫長的復元路上。為了鼓勵國人再站起來，這部由<span class="annotated" data-note="新海誠是日本著名的動畫導演，以唯美的畫風和富有詩意的劇情聞名。">新海誠</span>執導的電影《鈴芽之旅》，便從療癒面向探討地震的災後復甦。</p>

        <h2>結合地震、海嘯、核災、火災的複合型災害</h2>
        
        <p>在電影一開始，可以看到幼年時期的女主角鈴芽在殘破不堪的市區裡，不斷奔走尋找媽媽的身影，畫面呈現船在屋頂上、瓦礫在地上，天地顛倒的奇幻感。</p>

        <p><span class="annotated" data-note="311大地震發生於2011年3月11日，是日本有記錄以來最強烈的地震。">311大地震</span>不只是一場地震災害，同時也引發嚴重的海嘯，以及受海嘯造成的福島第一核電廠氣爆、輻射外洩汙染，甚至都市大火等複雜問題。在災區中，巨大的海嘯衝上好幾層樓高，把許多建築物摧毀，同時也破壞了核電廠的冷卻水設備，導致爐心無法冷卻、持續加熱，使水蒸發成水蒸氣，體積膨脹1,700倍，甚至進行劇烈的氧化還原反應，產生大量氫氣，終至氫爆。此外，日本建築常用木材搭建，考量其彈性與輕量可減緩地震災情，然而在<span class="annotated" data-note="氣仙沼市是日本宮城縣的一個市，在311大地震中遭受了嚴重的損害。">氣仙沼市</span>卻因為海嘯沖毀岸邊23座儲油槽，使大量重油漫延，引發長達兩週的嚴重火災，損失難以估計。</p>

        <h2>日本的地震傳說</h2>

        <p>在《鈴芽之旅》中，地震被描述為潛伏在另一個世界的大蚯蚓穿過「門」，導致現實世界發生災害，必須透過傳說中的古老職業「關門師」來阻止，並以<span class="annotated" data-note="要石是日本民間傳說中用來鎮壓地震的石頭。">要石</span>封印，遏止災害發生。現實中，日本及各個位於地震帶上的國家與民族，自古以來都有許多關於地震發生原因的傳說，如臺灣的「地牛翻身」、印度神話的「負地象」、希臘神話的「海神波賽頓」、中國山海經的「鰲魚」等。</p>

        <p>古代日本認為日本列島是由地底下的巨大<span class="annotated" data-note="鯰魚在日本民間傳說中被認為是引起地震的原因。">鯰魚</span>背負著，所以當鯰魚移動身體或搖擺魚尾，就會發生地震。為了使巨鯰不要作怪，必須透過建御雷神（或稱鹿島明神）以要石鎮壓。「要石」是引自真正的日本傳說，只是沒有如電影中所描述那樣會到處亂跑。但為什麼是透過雷神來鎮壓地震呢？過去地震也被認為是「地鳴」發生，與雷鳴相似，雷鳴來自天上、地鳴來自地下，因此被連結起來。1855年安政時期發生江戶大地震，以鎮壓地震鯰為主題的<span class="annotated" data-note="鯰繪是江戶時代流行的一種木版畫，常以諷刺的方式描繪地震和鯰魚的關係。">鯰繪</span>大為流行，也因此強化這個傳說。</p>

        <h2>與地震共存千年的生死輪迴</h2>

        <p>過去任何以地震為主題的電影，怎麼可能放過天崩地裂、海嘯、火山噴發，以及建築物倒塌壓傷人們的畫面，這是以往好萊塢式災難片的視覺刺激。《鈴芽之旅》雖然也是一部以地震為主題的電影，但為了減少災民對於災區畫面引發的創傷後壓力症候群（PTSD），沒有出現任何一幕震災的畫面，取而代之的是數幕寂靜的廢墟與繁華熱鬧的都市場景對比。</p>

        <p>繁榮的街景有兩層涵義，第一層是電影角色所說：「你不救他們嗎？如果地震發生了可是有數百萬人要死了喔！」這些人車雜沓的畫面，同時也代表著無數的生命，一但地震發生後果不堪設想。第二層則是要從日本這個數千年來與地震共存的國家來說，從九州、到四國、到淡路明石跨海大橋、再到東京，哪裡沒發生過地震，每一個地區都在阪神大地震、關東大地震後的廢墟中重建起來，象徵日本的死與新生，與地震共存的平衡，一代人死了，又有一代人站起來，在這塊土地上不斷建立起繁榮的景觀。</p>

        <p>電影最後回到日本東北，我們看到了311大地震的十二年後，仍然是滿目瘡痍、百廢待興，昔日的建築成了廢墟，以及清運輻射汙染廢土的巨大工地。高大的海堤擋住了海，本來親近的海岸已在人們的視線之外。「什麼時候，東北地方才能再站起來呢？十二年了啊！東北加油啊！」是這些畫面裡面沒說出口的臺詞。</p>

        <p>在以地震為主題的電影裡，不放譁眾取寵的震災畫面，而是用生離死別的親情、倖存者內疚，以及不斷從震災裡走出來的繁榮城市呈現，這是<span class="annotated" data-note="新海誠用溫柔的方式處理地震主題，避免直接展示震災畫面，而是通過其他方式表現地震的影響。">導演新海誠的溫柔</span>。</p>
    </div>

    <script>
        // 註釋功能
        document.querySelectorAll('.annotated').forEach(item => {
            item.addEventListener('click', event => {
                const note = event.target.getAttribute('data-note');
                let noteElement = event.target.nextElementSibling;
                
                if (!noteElement || !noteElement.classList.contains('note')) {
                    noteElement = document.createElement('div');
                    noteElement.className = 'note';
                    event.target.parentNode.insertBefore(noteElement, event.target.nextSibling);
                }
                
                noteElement.textContent = note;
                noteElement.style.display = noteElement.style.display === 'none' ? 'block' : 'none';
            });
        });

        // 語音朗讀功能
        let speechSynthesis = window.speechSynthesis;
        let speechUtterance = new SpeechSynthesisUtterance();
        let isPaused = false;
        let currentParagraph = null;

        function setupSpeech() {
            speechUtterance.lang = 'zh-TW';
            let voices = speechSynthesis.getVoices();
            let chineseVoice = voices.find(voice => voice.lang === 'zh-TW');
            if (chineseVoice) {
                speechUtterance.voice = chineseVoice;
            }
        }

        if (speechSynthesis.onvoiceschanged !== undefined) {
            speechSynthesis.onvoiceschanged = setupSpeech;
        }

        function togglePlayPause() {
            if (speechSynthesis.speaking) {
                if (isPaused) {
                    speechSynthesis.resume();
                    isPaused = false;
                    document.getElementById('playPauseBtn').textContent = '暫停';
                } else {
                    speechSynthesis.pause();
                    isPaused = true;
                    document.getElementById('playPauseBtn').textContent = '繼續';
                }
            } else {
                startReading();
                document.getElementById('playPauseBtn').textContent = '暫停';
            }
        }

        function startReading(paragraph = null) {
            stopReading();
            if (paragraph) {
                currentParagraph = paragraph;
            } else if (!currentParagraph) {
                currentParagraph = document.querySelector('#reading-container p');
            }
            speechUtterance.text = currentParagraph.textContent;
            speechSynthesis.speak(speechUtterance);
            isPaused = false;
            document.getElementById('playPauseBtn').textContent = '暫停';

            speechUtterance.onend = () => {
                currentParagraph = currentParagraph.nextElementSibling;
                if (currentParagraph && currentParagraph.tagName === 'P') {
                    startReading(currentParagraph);
                } else {
                    document.getElementById('playPauseBtn').textContent = '播放';
                    currentParagraph = null;
                }
            };
        }

        function stopReading() {
            speechSynthesis.cancel();
            isPaused = false;
            document.getElementById('playPauseBtn').textContent = '播放';
        }

        function changeSpeed(speed) {
            speechUtterance.rate = parseFloat(speed);
            document.getElementById('speed-value').textContent = speed + 'x';
            if (speechSynthesis.speaking) {
                const currentText = speechUtterance.text;
                stopReading();
                speechUtterance.text = currentText;
                speechSynthesis.speak(speechUtterance);
            }
        }

        // 點擊段落開始閱讀
        document.querySelectorAll('#reading-container p').forEach(paragraph => {
            paragraph.addEventListener('click', () => {
                startReading(paragraph);
            });
        });
    </script>

<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>《鈴芽之旅》閱讀理解測驗</title>
    <style>
        body {
            font-family: "Microsoft JhengHei", Arial, sans-serif;
            line-height: 1.6;
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }
        h1 {
            color: #333;
        }
        .question {
            margin-bottom: 20px;
            border: 1px solid #ddd;
            padding: 15px;
            border-radius: 5px;
        }
        .options {
            margin-left: 20px;
        }
        .feedback {
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            display: none;
        }
        .correct {
            background-color: #d4edda;
            color: #155724;
        }
        .incorrect {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
    <h1>《鈴芽之旅》閱讀理解測驗</h1>
    
    <div id="quiz">
        <div class="question">
            <p>1. 根據文章，311大地震是一個什麼樣的災害？</p>
            <div class="options">
                <label><input type="radio" name="q1" value="a"> a) 單純的地震災害</label><br>
                <label><input type="radio" name="q1" value="b"> b) 地震和海嘯的雙重災害</label><br>
                <label><input type="radio" name="q1" value="c"> c) 地震、海嘯、核災、火災的複合型災害</label><br>
                <label><input type="radio" name="q1" value="d"> d) 主要是核電站爆炸造成的災害</label>
            </div>
            <div class="feedback"></div>
        </div>

        <div class="question">
            <p>2. 在《鈴芽之旅》中，地震被描述為什麼？</p>
            <div class="options">
                <label><input type="radio" name="q2" value="a"> a) 地殼運動的結果</label><br>
                <label><input type="radio" name="q2" value="b"> b) 大蚯蚓穿過「門」導致的災害</label><br>
                <label><input type="radio" name="q2" value="c"> c) 神明的懲罰</label><br>
                <label><input type="radio" name="q2" value="d"> d) 自然界的正常現象</label>
            </div>
            <div class="feedback"></div>
        </div>

        <div class="question">
            <p>3. 根據文章，日本古代傳說中，是什麼動物導致地震的發生？</p>
            <div class="options">
                <label><input type="radio" name="q3" value="a"> a) 大象</label><br>
                <label><input type="radio" name="q3" value="b"> b) 鯨魚</label><br>
                <label><input type="radio" name="q3" value="c"> c) 鯰魚</label><br>
                <label><input type="radio" name="q3" value="d"> d) 龍</label>
            </div>
            <div class="feedback"></div>
        </div>

        <div class="question">
            <p>4. 《鈴芽之旅》這部電影在處理地震主題時有什麼特別之處？</p>
            <div class="options">
                <label><input type="radio" name="q4" value="a"> a) 展示了大量震撼的災難場面</label><br>
                <label><input type="radio" name="q4" value="b"> b) 完全避免了任何與地震相關的畫面</label><br>
                <label><input type="radio" name="q4" value="c"> c) 沒有直接展示震災畫面，而是通過對比和隱喻來表現</label><br>
                <label><input type="radio" name="q4" value="d"> d) 主要聚焦於地震預警系統的科技創新</label>
            </div>
            <div class="feedback"></div>
        </div>

        <div class="question">
            <p>5. 文章最後提到的「導演新海誠的溫柔」指的是什麼？</p>
            <div class="options">
                <label><input type="radio" name="q5" value="a"> a) 他在電影中加入了大量溫馨的場景</label><br>
                <label><input type="radio" name="q5" value="b"> b) 他避免了直接展示震災畫面，而是通過其他方式表現地震主題</label><br>
                <label><input type="radio" name="q5" value="c"> c) 他在電影中完全迴避了地震這個話題</label><br>
                <label><input type="radio" name="q5" value="d"> d) 他在電影中加入了許多安慰災民的情節</label>
            </div>
            <div class="feedback"></div>
        </div>
    </div>

    <script>
        const correctAnswers = {
            q1: 'c',
            q2: 'b',
            q3: 'c',
            q4: 'c',
            q5: 'b'
        };

        const feedbackMessages = {
            q1: {
                correct: "做得好！311大地震確實是一個複合型災害，包括地震、海嘯、核災和火災。",
                incorrect: "再想想看，311大地震不只是單一類型的災害。文章中提到了哪些不同類型的災害？"
            },
            q2: {
                correct: "正確！電影中確實將地震描述為大蚯蚓穿過「門」導致的災害。",
                incorrect: "仔細回想一下電影中對地震的描述。有提到什麼特別的生物嗎？"
            },
            q3: {
                correct: "沒錯！日本古代傳說中，正是鯰魚的活動導致了地震的發生。",
                incorrect: "這個問題的答案與日本的特定傳說有關。再仔細看看文章中提到的動物。"
            },
            q4: {
                correct: "很好！《鈴芽之旅》確實採用了一種獨特的方式來表現地震主題。",
                incorrect: "想想看，文章中是如何描述這部電影處理地震主題的方式？有提到直接展示災難場面嗎？"
            },
            q5: {
                correct: "你理解得很好！新海誠導演確實展現了一種特別的溫柔。",
                incorrect: "再想想看，文章最後部分提到了新海誠導演如何處理地震主題。他是否直接展示了震災畫面？"
            }
        };

        document.querySelectorAll('input[type="radio"]').forEach(radio => {
            radio.addEventListener('change', function() {
                const questionName = this.name;
                const selectedValue = this.value;
                const feedbackElement = this.closest('.question').querySelector('.feedback');
                
                if (selectedValue === correctAnswers[questionName]) {
                    feedbackElement.textContent = feedbackMessages[questionName].correct;
                    feedbackElement.className = 'feedback correct';
                } else {
                    feedbackElement.textContent = feedbackMessages[questionName].incorrect;
                    feedbackElement.className = 'feedback incorrect';
                }
                feedbackElement.style.display = 'block';
            });
        });
    </script>
</body>
</html>

<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>日本地震傳說配對遊戲</title>
    <style>
        body {
            font-family: "Microsoft JhengHei", Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            background-color: #f0f0f0;
        }
        #game-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        #game-board {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-top: 20px;
        }
        .card {
            width: 100px;
            height: 100px;
            perspective: 1000px;
            cursor: pointer;
        }
        .card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            text-align: center;
            transition: transform 0.3s;
            transform-style: preserve-3d;
        }
        .card.flipped .card-inner {
            transform: rotateY(180deg);
        }
        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 5px;
            font-size: 14px;
            color: white;
            transition: background-color 0.3s;
        }
        .card-front {
            background-color: #3498db;
        }
        .card-back {
            background-color: #2ecc71;
            transform: rotateY(180deg);
        }
        .card.matched .card-back {
            background-color: #f1c40f;
        }
        .card.mismatched .card-back {
            background-color: #e74c3c;
        }
        #info-panel {
            display: flex;
            justify-content: space-between;
            width: 100%;
            margin-bottom: 20px;
        }
        #difficulty-select {
            margin-bottom: 20px;
        }
  
