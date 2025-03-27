<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>單字卡學習</title>
    <style>
        body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background: linear-gradient(135deg, #f5f7fa 0%, #e4e9f2 100%);
}

.tv-container {
    width: 375px;
    height: 700px;
    background: white;
    border-radius: 24px;
    box-shadow: 
        0 10px 20px rgba(0,0,0,0.08),
        0 0 0 1px rgba(0,0,0,0.04);
    padding: 20px;
    position: relative;
    display: flex;
    flex-direction: column;
}

.tv-screen {
    width: 100%;
    height: 460px;
    background: #f8fafc;
    border-radius: 20px;
    overflow: hidden;
    position: relative;
    box-shadow: 
        inset 0 2px 4px rgba(0, 0, 0, 0.05),
        0 1px 3px rgba(0, 0, 0, 0.08);
    padding: 2px;
    box-sizing: border-box;
}

.flashcard-container {
    width: 100%;
    height: 100%;
    position: relative;
    perspective: 1500px;
}

.flashcard {
    width: 100%;
    height: 100%;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

.flashcard.flip-right,
.flashcard.flip-left {
    transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1);
}

/* 為不同狀態的卡片添加微妙的邊框顏色變化 */
.card:nth-child(1) {
    border-color: rgba(79, 70, 229, 0.3);
}

.card:nth-child(2) {
    border-color: rgba(79, 70, 229, 0.4);
}

.card:nth-child(3) {
    border-color: rgba(79, 70, 229, 0.5);
}

.card {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: white;
    border-radius: 20px;
    padding: 20px;
    box-sizing: border-box;
    overflow: hidden;
    /* 加強邊框和陰影效果 */
    border: 2px solid #e2e8f0;
    box-shadow: 
        0 4px 6px rgba(0, 0, 0, 0.05),
        0 10px 15px rgba(0, 0, 0, 0.1),
        0 0 0 2px rgba(79, 70, 229, 0.1);
    /* 添加漸變背景 */
    background: linear-gradient(
        to bottom right,
        #ffffff 0%,
        #fafaff 100%
    );
}

/* 當卡片翻轉時保持邊框效果 */
.card.back {
    transform: rotateY(180deg);
    border: 2px solid #e2e8f0;
}

.flashcard:hover .card {
    box-shadow: 
        0 6px 8px rgba(0, 0, 0, 0.07),
        0 12px 17px rgba(0, 0, 0, 0.12),
        0 0 0 3px rgba(79, 70, 229, 0.15);
    border: 2px solid #d1d5f0;
    transition: all 0.3s ease;
}

.word {
    font-size: clamp(24px, 5vw, 40px);
    font-weight: 700;
    text-align: center;
    color: #1a1a1a;
    width: 100%;
    margin-bottom: 16px;
    padding: 0 16px;
    box-sizing: border-box;
    line-height: 1.2;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 60px;
    overflow-wrap: break-word;
    word-wrap: break-word;
    hyphens: auto;
    transition: transform 0.3s ease;
}

.meaning {
    font-size: clamp(18px, 4vw, 24px);
    margin-top: 20px;
    color: #1a1a1a;
    text-align: center;
    padding: 0 16px;
    line-height: 1.4;
}

.example-container {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    padding: 16px;
    box-sizing: border-box;
}

.image-container {
    width: 100%;
    height: 35%;
    min-height: 120px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 16px;
    border-radius: 16px;
    background: #f4f4f5;
    overflow: hidden;
}

.image-container img {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
}

.example-text {
    flex: 1;
    overflow-y: auto;
    padding: 0 8px;
}

.example {
    font-size: clamp(16px, 3.5vw, 18px);
    line-height: 1.6;
    color: #1a1a1a;
    margin: 0 0 12px 0;
    overflow-wrap: break-word;
    word-wrap: break-word;
    text-align: justify;
    hyphens: none;
}

.translation-container {
    border-radius: 0.75rem;
    background: linear-gradient(180deg, rgba(79, 70, 229, 0.08) 0%, rgba(255, 255, 255, 1) 100%);
    transition: all 0.3s ease-out;
    cursor: pointer;
    overflow: hidden;
    min-height: 32px;
}

.translation-container:hover {
    background: linear-gradient(180deg, rgba(79, 70, 229, 0.12) 0%, rgba(79, 70, 229, 0.08) 100%);
}

.translation {
    display: none;
    font-size: clamp(14px, 3vw, 16px);
    text-align: left;
    color: #4b5563;
    line-height: 1.6;
    padding: 12px;
    margin: 0;
    width: 100%;
    box-sizing: border-box;
    white-space: normal;
    word-wrap: break-word;
}

.translation-hint {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 32px;
}

.translation-arrow {
    width: 24px;
    height: 24px;
    stroke-width: 2.5;
    color: rgba(79, 70, 229, 0.7);
    transition: all 0.3s;
    animation: bounce-gentle 1.5s ease-in-out infinite;
}

.translation-container:hover .translation-arrow {
    color: rgba(79, 70, 229, 1);
    transform: translateY(4px);
}

.translation-container.show {
    background-color: rgba(79, 70, 229, 0.08);
    box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.05);
}

.translation-container.show .translation {
    display: block;
}

.translation-container.show .translation-hint {
    display: none;
}

/* 滾動條樣式 */
.example-text::-webkit-scrollbar {
    width: 4px;
}

.example-text::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 2px;
}

.example-text::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 2px;
}

.example-text::-webkit-scrollbar-thumb:hover {
    background: #555;
}

@keyframes bounce-gentle {
    0%, 100% {
        transform: translateY(0);
    }
    50% {
        transform: translateY(4px);
    }
}

.card-indicators {
    display: flex;
    justify-content: center;
    gap: 8px;
    position: absolute;
    bottom: 20px;
    left: 0;
    right: 0;
}

.indicator {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: #e4e4e7;
    transition: all 0.3s ease;
    cursor: pointer;
}

.indicator.active {
    background-color: #4f46e5;
    transform: scale(1.2);
}

.tv-controls {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    gap: 12px;
    padding: 20px 0 0 0;
}

.controls-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 12px;
}

.category-buttons {
    display: flex;
    gap: 8px;
    justify-content: center;
    flex-grow: 1;
}

.category-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 20px;
    background-color: #f4f4f5;
    color: #666;
    cursor: pointer;
    transition: all 0.2s ease;
    font-size: 14px;
    font-weight: 500;
    white-space: nowrap;
}

.category-btn.active {
    background-color: #4f46e5;
    color: white;
}

.tv-button {
    width: 50px;
    height: 50px;
    border-radius: 16px;
    background-color: #4f46e5;
    border: none;
    cursor: pointer;
    font-size: 24px;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: all 0.2s ease;
}

.tv-button:hover {
    background-color: #4338ca;
    transform: scale(1.05);
}

.tv-button.list {
    background-color: #4f46e5;
    width: 100%;
    padding: 0 20px;
    border-radius: 16px;
    font-size: 16px;
    height: 56px;
    font-weight: 600;
}

.syllables-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    width: 100%;
    gap: 4px;
    padding: 8px;
    box-sizing: border-box;
}

.syllable {
    display: inline-block;
    padding: 2px 4px;
    font-size: clamp(20px, 4vw, 36px);
    line-height: 1.2;
    white-space: normal;
    text-align: center;
    transition: color 0.3s, font-size 0.3s;
}

.syllable-separator {
    margin: 0 2px;
    color: #666;
    font-size: clamp(16px, 3vw, 24px);
}

.highlight {
    color: #4f46e5;
    transform: scale(1.1);
}

/* Modal styles */
.modal {
    display: none;
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0,0,0,0.4);
    animation: fadeIn 0.3s ease;
}

.modal-content {
    background-color: #fefefe;
    margin: 15% auto;
    padding: 24px;
    border: none;
    width: 80%;
    max-width: 300px;
    border-radius: 20px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    animation: slideIn 0.3s ease;
}

.close {
    color: #666;
    float: right;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    line-height: 1;
    transition: all 0.2s ease;
}

.close:hover,
.close:focus {
    color: #1a1a1a;
    text-decoration: none;
}

#wordListItems {
    list-style-type: none;
    padding: 0;
    margin: 16px 0 0 0;
    max-height: 300px;
    overflow-y: auto;
}

#wordListItems li {
    padding: 12px 16px;
    cursor: pointer;
    border-bottom: 1px solid #f4f4f5;
    color: #1a1a1a;
    transition: all 0.2s ease;
    font-size: 16px;
}

#wordListItems li:last-child {
    border-bottom: none;
}

#wordListItems li:hover {
    background-color: #f4f4f5;
    padding-left: 20px;
}



/* Animations */
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

@keyframes slideIn {
    from { transform: translateY(-20px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
}

@keyframes flipRight {
    from { transform: rotateY(0deg); }
    to { transform: rotateY(-180deg); }
}

@keyframes flipLeft {
    from { transform: rotateY(0deg); }
    to { transform: rotateY(180deg); }
}

/* Responsive design */
@media screen and (max-width: 375px) {
    .tv-container {
        width: 100%;
        height: 100vh;
        border-radius: 0;
        padding: 16px;
    }
    
    .word {
        font-size: clamp(20px, 4.5vw, 32px);
        padding: 0 12px;
    }
    
    .syllable {
        font-size: clamp(18px, 3.5vw, 28px);
        padding: 1px 2px;
    }
    
    .category-btn {
        padding: 6px 12px;
        font-size: 13px;
    }
    
    .tv-button {
        width: 44px;
        height: 44px;
        font-size: 20px;
    }
}

/* Utility classes */
.auto-scale {
    transform-origin: center center;
    transition: transform 0.3s ease;
}

.prevent-select {
    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

.smooth-transition {
    transition: all 0.3s ease;
}
    .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
    position: relative;
    padding: 0 4px;
    min-height: 32px; /* 確保標題有足夠的空間 */
}

.header h1 {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    margin: 0;
    font-size: 16px; /* 稍微縮小字體 */
    color: #1a1a1a;
    font-weight: 600;
    white-space: nowrap; /* 防止文字換行 */
    overflow: hidden; /* 防止溢出 */
    text-overflow: ellipsis; /* 文字溢出時顯示省略號 */
    max-width: 60%; /* 限制最大寬度，確保不會擋到按鈕 */
}

.button-group {
    margin-left: auto;
    display: flex;
    gap: 8px;
    z-index: 1;
}

.header-btn {
    background: none;
    border: none;
    font-size: 18px; /* 稍微縮小按鈕大小 */
    padding: 4px;
    cursor: pointer;
    text-decoration: none;
    color: #4f46e5;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: transform 0.2s ease;
}

.header-btn:hover {
    transform: scale(1.1);
}

/* 導覽 Modal 樣式 */
.guide-modal {
    display: none;
    position: fixed;
    z-index: 2000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
    animation: fadeIn 0.3s ease;
}

.guide-content {
    position: relative;
    background-color: white;
    margin: 15% auto;
    padding: 24px;
    width: 80%;
    max-width: 320px;
    border-radius: 16px;
    animation: slideIn 0.3s ease;
}

.guide-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.guide-header h2 {
    margin: 0;
    font-size: 20px;
    color: #1a1a1a;
}

.close-guide {
    font-size: 24px;
    color: #666;
    cursor: pointer;
    line-height: 1;
}

.guide-item {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 16px;
    padding: 12px;
    background-color: #f8fafc;
    border-radius: 8px;
}

.guide-icon {
    font-size: 20px;
    width: 24px;
    text-align: center;
}

.guide-item p {
    margin: 0;
    color: #4a5568;
    font-size: 14px;
}

.guide-close-btn {
    width: 100%;
    padding: 12px;
    background-color: #4f46e5;
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    margin-top: 16px;
    transition: background-color 0.2s ease;
}

.guide-close-btn:hover {
    background-color: #4338ca;
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

@keyframes slideIn {
    from { transform: translateY(-20px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
}
.example span {
    display: inline-block;
    padding: 2px 4px;
    margin: 0 -1px;
    border-radius: 4px;
    transition: all 0.3s ease;
}

.example span.highlight {
    background-color: rgba(79, 70, 229, 0.1);
    color: #4f46e5;
    transform: scale(1.05);
}

.example span.highlight-word {
    color: #4f46e5;
    font-weight: 600;
}

.highlight-word {
    color: #4f46e5;
    font-weight: 700; /* 提升粗體效果從 600 到 700 */
}
/* 添加在 style 標籤內的最末尾 */
.speech-modal-content {
    max-width: 320px;
    padding: 24px;
    text-align: center;
}

.target-word {
    font-size: 32px;
    font-weight: 700;
    margin-bottom: 20px;
    color: #1a1a1a;
}

.speech-feedback {
    margin-bottom: 20px;
    min-height: 120px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.waveform-container {
    width: 100%;
    height: 60px;
    background: #f8f9fa;
    border-radius: 12px;
    margin-bottom: 16px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
}

.waveform {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}

.waveform.active {
    display: flex;
    align-items: center;
    justify-content: center;
}

.wave-bar {
    width: 4px;
    height: 5px;
    margin: 0 2px;
    background: #4f46e5;
    border-radius: 2px;
    transition: height 0.1s ease;
}

.recognition-result {
    font-size: 18px;
    margin-bottom: 8px;
    min-height: 27px;
}

.accuracy-score {
    font-size: 24px;
    font-weight: 600;
    margin-bottom: 16px;
    min-height: 36px;
}

.accuracy-score.high {
    color: #10b981;
}

.accuracy-score.medium {
    color: #f59e0b;
}

.accuracy-score.low {
    color: #ef4444;
}

.speech-btn {
    width: 100%;
    height: 56px;
    border-radius: 16px;
    background-color: #4f46e5;
    border: none;
    color: white;
    font-size: 16px;
    font-weight: 600;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: all 0.2s ease;
    position: relative;
    overflow: hidden;
}

.speech-btn:hover {
    background-color: #4338ca;
}

.speech-btn:active {
    transform: scale(0.98);
}

.speech-btn.recording {
    background-color: #ef4444;
}

.record-icon {
    margin-right: 8px;
    font-size: 20px;
}

.record-text {
    transition: all 0.2s ease;
}

.ripple {
    position: absolute;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.3);
    transform: scale(0);
    animation: ripple-animation 0.6s linear;
}

@keyframes ripple-animation {
    to {
        transform: scale(4);
        opacity: 0;
    }
}

.syllable-feedback {
    display: flex;
    justify-content: center;
    gap: 2px;
    margin-top: 12px;
}

.syllable-item {
    padding: 4px 8px;
    border-radius: 4px;
    font-size: 16px;
}

.syllable-item.correct {
    background-color: rgba(16, 185, 129, 0.1);
    color: #10b981;
}

.syllable-item.incorrect {
    background-color: rgba(239, 68, 68, 0.1);
    color: #ef4444;
}

.speech-icon {
    position: absolute;
    right: 12px;
    bottom: 12px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #4f46e5;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: all 0.2s ease;
    z-index: 10;
}

.speech-icon:hover {
    background-color: #4338ca;
    transform: scale(1.05);
}

.speech-close {
    position: absolute;
    right: 20px;
    top: 20px;
}
</style>
</head>
<body>

    <div class="tv-container">
    <div class="header">
        <h1> L01 Say Hello to Your Future </h1>
        <div class="button-group">
            <a href=" https://sites.google.com/view/main-unit-6-lt/%E9%A6%96%E9%A0%81" class="header-btn home-btn" target="_blank">🏠</a>
            <button class="header-btn guide-btn" onclick="showGuide()">💡</button>
        </div>
    </div>
    <div class="tv-screen">
        <div class="flashcard-container">
            <div class="flashcard" id="flashcard">
                <div class="card" id="card1">
                    <div class="word" id="wordDisplay"></div>
                </div>
                <div class="card" id="card2">
                    <div class="word" id="wordBack"></div>
                    <div class="meaning" id="meaningDisplay"></div>
                </div>
                <div class="card" id="card3">
                    <div class="example-container">
                        <div class="image-container" id="imageContainer">
                            圖片預留區
                        </div>
                        <div class="example-text">
                            <div class="example" id="exampleDisplay"></div>
                            <div class="translation" id="translationDisplay"></div>
                        </div>
                    </div>
                </div>
                <div class="card " id="card4">
                    <div class="example-container">
                        <div class="image-container" id="imageContainer2">
                            圖片預留區
                        </div>
                        <div class="example-text">
                            <div class="example" id="exampleDisplay2"></div>
                            <div class="translation" id="translationDisplay2"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="card-indicators">
            <span class="indicator"></span>
            <span class="indicator"></span>
            <span class="indicator"></span>
            <span class="indicator"></span>
        </div>
    </div>
    <div class="tv-controls">
        <div class="controls-row">
            <button class="tv-button" id="prevWord">◀</button>
            <div class="category-buttons">
    <button class="category-btn active" data-category="words">單字</button>
    <button class="category-btn" data-category="idioms">片語</button>
</div>
            <button class="tv-button" id="nextWord">▶</button>
        </div>
        <div class="controls-row">
            <button class="tv-button list" id="wordListBtn">單字列表</button>
        </div>
    </div>
</div>

    <div id="wordListModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>單字列表</h2>
            <ul id="wordListItems"></ul>
        </div>
    </div>
        <div id="guideModal" class="modal guide-modal">
    <div class="modal-content guide-content">
        <div class="guide-header">
            <h2>使用導覽</h2>
            <span class="close-guide" onclick="hideGuide()">&times;</span>
        </div>
        <div class="guide-body">
            <div class="guide-item">
                <span class="guide-icon">👆</span>
                <p>左右滑動切換單字卡面</p>
            </div>
            <div class="guide-item">
                <span class="guide-icon">🔄</span>
                <p>點擊箭頭按鈕切換單字</p>
            </div>
            <div class="guide-item">
                <span class="guide-icon">🔊</span>
                <p>自動播放單字發音</p>
            </div>
            <div class="guide-item">
                <span class="guide-icon">📝</span>
                <p>可切換單字、片語、認知詞彙</p>
            </div>
        </div>
        <button class="guide-close-btn" onclick="hideGuide()">知道了！</button>
    </div>
</div>
    
<!-- 在 <div id="wordListModal" class="modal"> 後面添加 -->
<div id="speechRecognitionModal" class="modal">
    <div class="modal-content speech-modal-content">
        <span class="close speech-close">&times;</span>
        <h2>發音練習</h2>
        <div class="speech-content">
            <div class="target-word"></div>
            <div class="speech-feedback">
                <div class="waveform-container">
                    <div class="waveform"></div>
                </div>
                <div class="recognition-result"></div>
                <div class="accuracy-score"></div>
            </div>
            <button class="speech-btn" id="recordButton">
                <span class="record-icon">🎤</span>
                <span class="record-text">按住說話</span>
            </button>
        </div>
    </div>
</div>
    <script>
        const vocabularyData = {
    words: [
        {
            word: "exciting",
            meaning: "adj. 令人興奮的；刺激的",
            example: "Tony watched an exciting live basketball game last night.",
            translation: "Tony昨晚看了一場令人興奮的籃球現場直播。",
            syllables: ["ex", "ci", "ting"],
            pronunciationGuide: ["ɪk", "saɪ", "tɪŋ"],
            image: "https://hackmd.io/_uploads/BJSVVGtLkg.png"
        },
        {
            word: "excited",
            meaning: "adj. 興奮的",
            example: "All the students are excited about the field trip.",
            translation: "所有的學生都對這次校外教學感到興奮。",
            syllables: ["ex", "ci", "ted"],
            pronunciationGuide: ["ɪk", "saɪ", "tɪd"],
            image: "https://hackmd.io/_uploads/ryzF9zFIkg.png"
        },
        {
            word: "proud",
            meaning: "adj. 驕傲的",
            example: "",
            translation: "",
            syllables: ["proud"],
            pronunciationGuide: ["praʊd"],
            image: "https://hackmd.io/_uploads/Bkl3cMF8yg.png"
        },
        {
            word: "challenge",
            meaning: "n. [C] 挑戰",
            example: "Henry always faces challenges in a brave way.",
            translation: "Henry總是勇敢地面對挑戰。",
            syllables: ["chal", "lenge"],
            pronunciationGuide: ["tʃæ", "lɪndʒ"],
            image: "https://hackmd.io/_uploads/r1N1oGtLkl.png"
        },
        {
            word: "nervous",
            meaning: "adj. 緊張的",
            example: "Tom is nervous about the final exam.",
            translation: "Tom對期末考試感到緊張。",
            syllables: ["ner", "vous"],
            pronunciationGuide: ["nɝ", "vəs"],
            image: "https://hackmd.io/_uploads/ryNGjMF8Jx.png"
        },
        {
            word: "different",
            meaning: "adj. 不同的",
            example: "Asian elephants are different from African elephants.",
            translation: "亞洲象和非洲象是不同的。",
            syllables: ["dif", "fer", "ent"],
            pronunciationGuide: ["dɪ", "fər", "ənt"],
            image: "https://hackmd.io/_uploads/r1NBjzKLyx.png"
        },
        {
            word: "difference",
            meaning: "n. [U, C] 差異",
            example: "There is little difference in looks between the two sisters.",
            translation: "這兩姊妹的長相幾乎沒有差異。",
            syllables: ["dif", "fer", "ence"],
            pronunciationGuide: ["dɪ", "fər", "əns"],
            image: "https://hackmd.io/_uploads/S1nPsfKI1e.png"
        },
        {
            word: "awesome",
            meaning: "adj. 很棒的；令人驚歎的",
            example: "The magic show was awesome. I enjoyed it a lot.",
            translation: "這場魔術表演很精彩。我很享受。",
            syllables: ["awe", "some"],
            pronunciationGuide: ["ɔ", "səm"],
            image: "https://hackmd.io/_uploads/BJ6KszYI1e.png"
        },
        {
            word: "surprised",
            meaning: "adj. 驚訝的",
            example: "The fans were surprised at the famous singer's sudden marriage.",
            translation: "粉絲們對這位著名歌手突然結婚感到驚訝。",
            syllables: ["sur", "prised"],
            pronunciationGuide: ["sə", "praɪzd"],
            image: "https://hackmd.io/_uploads/S1XTjGFUJg.png"
        },
        {
            word: "surprise",
            meaning: "n. [C] 驚訝",
            example: "To our surprise, Andy won first place in the race.",
            translation: "令我們驚訝的是，Andy在比賽中獲得第一名。",
            syllables: ["sur", "prise"],
            pronunciationGuide: ["sɚ", "praɪz"],
            image: "https://hackmd.io/_uploads/rynBgXt8Jx.png"
        },
        {
            word: "interested",
            meaning: "adj. 有興趣的",
            example: "Steve is interested in playing the guitar.",
            translation: "Steve對彈吉他很有興趣。",
            syllables: ["in", "ter", "est", "ed"],
            pronunciationGuide: ["ɪn", "tər", "ɪs", "tɪd"],
            image: "https://hackmd.io/_uploads/HkWdemKIkl.png"
        },
        {
            word: "interesting",
            meaning: "adj. 有趣的",
            example: "Ms. White told the kids an interesting story.",
            translation: "White小姐給孩子們講了一個有趣的故事。",
            syllables: ["in", "ter", "est", "ing"],
            pronunciationGuide: ["ɪn", "tər", "ɪs", "tɪŋ"],
            image: "https://hackmd.io/_uploads/S1_5gQtU1l.png"
        },
        {
            word: "decision",
            meaning: "n. [C] 決定",
            example: "Before Judy makes a decision, she talks about it with her parents.",
            translation: "在Judy做決定之前，她會和父母討論。",
            syllables: ["de", "ci", "sion"],
            pronunciationGuide: ["dɪ", "sɪ", "ʒən"],
            image: "https://hackmd.io/_uploads/ry4agXFI1g.png"
        },
        {
            word: "decide",
            meaning: "vi. vt. 決定",
            example: "Stacy decided not to buy the dress because it was too expensive.",
            translation: "Stacy決定不買那件洋裝因為太貴了。",
            syllables: ["de", "cide"],
            pronunciationGuide: ["dɪ", "saɪd"],
            image: "https://hackmd.io/_uploads/H1-E-7F8kg.png"
        },
        {
            word: "upset",
            meaning: "adj. 難過的",
            example: "Hanna's cat died a few days ago, so she was quite upset.",
            translation: "Hanna的貓幾天前死了，所以她很難過。",
            syllables: ["up", "set"],
            pronunciationGuide: ["ʌp", "sɛt"],
            image: "https://hackmd.io/_uploads/rJSU-mtIyx.png"
        },
        {
            word: "trust",
            meaning: "vt. 相信；信任",
            example: "We can't trust Ben because he likes to tell lies.",
            translation: "我們無法相信Ben因為他愛說謊。",
            syllables: ["trust"],
            pronunciationGuide: ["trʌst"],
            image: "https://hackmd.io/_uploads/BkeK-QKL1x.png"
        },
        {
            word: "believe",
            meaning: "vt. 相信",
            example: "I can't believe it! I just took a picture with my favorite actor.",
            translation: "我不敢相信！我剛剛和我最喜歡的演員合照了。",
            syllables: ["be", "lieve"],
            pronunciationGuide: ["bɪ", "liv"],
            image: "https://hackmd.io/_uploads/SJvsZ7FIJe.png"
        },
        {
            word: "perfect",
            meaning: "adj. 完美的",
            example: "The weather today is perfect. Let's go to the beach!",
            translation: "今天的天氣很完美。讓我們去海灘吧！",
            syllables: ["per", "fect"],
            pronunciationGuide: ["pɝ", "fɪkt"],
            image: "https://hackmd.io/_uploads/SyWpb7KLyl.png"
        },
        {
            word: "certainly",
            meaning: "adv. 必定",
            example: "Joe studies very hard, so he will certainly pass the exam.",
            translation: "Joe很用功讀書，所以他一定會通過考試。",
            syllables: ["cer", "tain", "ly"],
            pronunciationGuide: ["sɝ", "tən", "lɪ"],
            image: "https://hackmd.io/_uploads/rky1M7t8yx.png"
        },
        {
            word: "unforgettable",
            meaning: "adj. 令人難忘的",
            example: "My one-month trip to Italy on my own was unforgettable.",
            translation: "我獨自一人在義大利的一個月旅行令人難忘。",
            syllables: ["un", "for", "get", "ta", "ble"],
            pronunciationGuide: ["ʌn", "fɚ", "gɛt", "ə", "bḷ"],
            image: "https://hackmd.io/_uploads/S1yzMmKL1l.png"
        },
        {
            word: "memory",
            meaning: "n. [C] 回憶；記憶",
            example: "Every time Anna looks at those photos, she thinks of the sweet memories of her high school life.",
            translation: "每當Anna看著那些照片，她就會想起高中生活的美好回憶。",
            syllables: ["mem", "o", "ry"],
            pronunciationGuide: ["mɛm", "ə", "rɪ"],
            image: "https://hackmd.io/_uploads/HJDEMQtLyx.png"
        }
    ],
    idioms: [
        {
            word: "be in the same boat",
            meaning: "處在相同困境",
            example: "The traffic is terrible, but since we all are in the same boat, we should not get angry.",
            translation: "雖然交通很糟糕，但既然我們都處在相同的困境，就不應該生氣。",
            image: "https://hackmd.io/_uploads/H1tH1l5I1e.png"
        },
        {
            word: "make a/the difference",
            meaning: "帶來不同；造成影響",
            example: "A good teacher can make a difference in her or his students' lives.",
            translation: "一個好老師能在學生的生命中帶來改變。",
            image: "https://hackmd.io/_uploads/rkX_JxcLkg.png"
        },
        {
            word: "go for sth.",
            meaning: "努力爭取某事物",
            example: "Every swimmer went for first prize in the swimming race.",
            translation: "每個游泳選手都在為游泳比賽的第一名努力。",
            image: "https://hackmd.io/_uploads/HyZsyl5L1x.png"
        },
        {
            word: "give up",
            meaning: "放棄",
            example: "Although the job is not easy, John never gives up.",
            translation: "雖然這份工作並不容易，但John從未放棄。",
            image: "https://hackmd.io/_uploads/HJRvMlcUkx.png"
        },
        {
            word: "have one's back",
            meaning: "支持某人",
            example: "Nancy decided to study in France, and her parents had her back.",
            translation: "Nancy決定到法國讀書，她的父母支持她。",
            image: "https://hackmd.io/_uploads/ByA9Ml5Uye.png"
        },
        {
            word: "all the time",
            meaning: "一直；總是",
            example: "Stacy asks questions all the time because she wants to know more about the world.",
            translation: "Stacy總是問問題，因為她想更了解這個世界。",
            image: "https://hackmd.io/_uploads/S1mCfl9I1e.png"
        }
    ] 
};


		let recognition;
let isRecording = false;
let audioContext;
let analyser;
let waveformBars = [];
let animationFrameId;

        let currentCategory = 'words';
        let currentCard = 0;
        let currentWordIndex = 0;
        const totalCards = 3;

        function getTotalCards(category) {
    if (category === 'recognition') {
        return 2;
    }
    // 目前的資料結構中沒有多例句，所以最多顯示3張卡片
    return 3;
}

		// 添加在 initializeFlashcards 函數之前
function initializeSpeechRecognition() {
    // 檢查瀏覽器是否支援語音辨識
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    if (!window.SpeechRecognition) {
        console.error('您的瀏覽器不支援語音辨識功能');
        return false;
    }
    
    recognition = new SpeechRecognition();
    recognition.lang = 'en-US';
    recognition.interimResults = false;
    recognition.maxAlternatives = 1;
    
    // 設置辨識結果處理函數
    recognition.onresult = handleSpeechResult;
    recognition.onerror = handleSpeechError;
    recognition.onend = handleSpeechEnd;
    
    // 初始化音頻分析器 (用於波形顯示)
    initializeAudioAnalyser();
    
    return true;
}

function initializeAudioAnalyser() {
    try {
        audioContext = new (window.AudioContext || window.webkitAudioContext)();
        analyser = audioContext.createAnalyser();
        analyser.fftSize = 256;
    } catch (error) {
        console.error('無法初始化音頻分析器', error);
    }
}

// 添加在 initializeSpeechRecognition 函數之後
function handleSpeechResult(event) {
    isRecording = false;
    stopWaveformAnimation();
    
    const speechBtn = document.getElementById('recordButton');
    speechBtn.classList.remove('recording');
    speechBtn.querySelector('.record-text').textContent = '按住說話';
    
    const resultDisplay = document.querySelector('.recognition-result');
    const scoreDisplay = document.querySelector('.accuracy-score');
    const transcript = event.results[0][0].transcript.toLowerCase().trim();
    const confidence = event.results[0][0].confidence;
    
    resultDisplay.textContent = `您說的是: "${transcript}"`;
    
    // 取得目標文字
    let targetText = '';
    if (currentCard === 1) {
        // 單字練習
        targetText = vocabularyData[currentCategory][currentWordIndex].word.toLowerCase();
    } else {
        // 例句練習
        if (vocabularyData[currentCategory][currentWordIndex].examples) {
            const exampleIndex = currentCard === 2 ? 0 : 1;
            if (vocabularyData[currentCategory][currentWordIndex].examples.length > exampleIndex) {
                targetText = vocabularyData[currentCategory][currentWordIndex].examples[exampleIndex].sentence.toLowerCase();
            }
        } else if (currentCard === 2 && vocabularyData[currentCategory][currentWordIndex].example) {
            targetText = vocabularyData[currentCategory][currentWordIndex].example.toLowerCase();
        }
    }
    
    // 文字相似度計算
    const similarity = calculateSimilarity(targetText, transcript);
    const percentScore = Math.round(similarity * 100);
    
    // 設置顏色等級
    let scoreClass = 'low';
    if (percentScore >= 80) {
        scoreClass = 'high';
    } else if (percentScore >= 60) {
        scoreClass = 'medium';
    }
    
    scoreDisplay.textContent = `準確度: ${percentScore}%`;
    scoreDisplay.className = 'accuracy-score ' + scoreClass;
    
    // 如果是單字練習，添加音節反饋
    if (currentCard === 1 && vocabularyData[currentCategory][currentWordIndex].syllables) {
        const syllablesContainer = document.createElement('div');
        syllablesContainer.className = 'syllable-feedback';
        
        const syllables = vocabularyData[currentCategory][currentWordIndex].syllables;
        const wordParts = splitTranscriptBySyllables(transcript, syllables);
        
        syllables.forEach((syllable, index) => {
            const syllableSpan = document.createElement('span');
            syllableSpan.className = 'syllable-item';
            syllableSpan.textContent = syllable;
            
            if (wordParts[index] && wordParts[index].match) {
                syllableSpan.classList.add('correct');
            } else {
                syllableSpan.classList.add('incorrect');
            }
            
            syllablesContainer.appendChild(syllableSpan);
        });
        
        // 清除先前的音節反饋
        const oldSyllableFeedback = document.querySelector('.syllable-feedback');
        if (oldSyllableFeedback) {
            oldSyllableFeedback.remove();
        }
        
        document.querySelector('.speech-feedback').appendChild(syllablesContainer);
    }
}

function handleSpeechError(event) {
    isRecording = false;
    stopWaveformAnimation();
    
    const speechBtn = document.getElementById('recordButton');
    speechBtn.classList.remove('recording');
    speechBtn.querySelector('.record-text').textContent = '按住說話';
    
    const resultDisplay = document.querySelector('.recognition-result');
    resultDisplay.textContent = '無法辨識您的語音，請再試一次';
    
    console.error('語音辨識錯誤:', event.error);
}

function handleSpeechEnd() {
    if (isRecording) {
        isRecording = false;
        stopWaveformAnimation();
        
        const speechBtn = document.getElementById('recordButton');
        speechBtn.classList.remove('recording');
        speechBtn.querySelector('.record-text').textContent = '按住說話';
    }
}

// 計算文字相似度 (使用 Levenshtein 距離)
function calculateSimilarity(str1, str2) {
    const track = Array(str2.length + 1).fill(null).map(() => 
        Array(str1.length + 1).fill(null));
    
    for (let i = 0; i <= str1.length; i += 1) {
        track[0][i] = i;
    }
    
    for (let j = 0; j <= str2.length; j += 1) {
        track[j][0] = j;
    }
    
    for (let j = 1; j <= str2.length; j += 1) {
        for (let i = 1; i <= str1.length; i += 1) {
            const indicator = str1[i - 1] === str2[j - 1] ? 0 : 1;
            track[j][i] = Math.min(
                track[j][i - 1] + 1, // deletion
                track[j - 1][i] + 1, // insertion
                track[j - 1][i - 1] + indicator, // substitution
            );
        }
    }
    
    const maxLength = Math.max(str1.length, str2.length);
    if (maxLength === 0) return 1.0;
    
    return 1 - (track[str2.length][str1.length] / maxLength);
}

// 將辨識結果按音節分割
function splitTranscriptBySyllables(transcript, syllables) {
    const result = [];
    let transcriptLower = transcript.toLowerCase();
    
    for (let i = 0; i < syllables.length; i++) {
        const syllable = syllables[i].toLowerCase();
        const index = transcriptLower.indexOf(syllable);
        
        if (index !== -1) {
            result.push({
                syllable: syllable,
                match: true
            });
            transcriptLower = transcriptLower.substring(index + syllable.length);
        } else {
            result.push({
                syllable: syllable,
                match: false
            });
        }
    }
    
    return result;
}

// 添加在前面函數之後
function createWaveform() {
    const waveformElement = document.querySelector('.waveform');
    waveformElement.innerHTML = '';
    waveformBars = [];
    
    const barCount = 30;
    
    for (let i = 0; i < barCount; i++) {
        const bar = document.createElement('div');
        bar.className = 'wave-bar';
        waveformElement.appendChild(bar);
        waveformBars.push(bar);
    }
}

function startWaveformAnimation() {
    const waveformElement = document.querySelector('.waveform');
    waveformElement.classList.add('active');
    
    function updateWaveform() {
        if (!isRecording) return;
        
        // 模擬麥克風輸入 (由於無法直接獲取麥克風輸入音量)
        for (let i = 0; i < waveformBars.length; i++) {
            const height = Math.floor(Math.random() * 25) + 5;
            waveformBars[i].style.height = `${height}px`;
        }
        
        animationFrameId = requestAnimationFrame(updateWaveform);
    }
    
    updateWaveform();
}

function stopWaveformAnimation() {
    const waveformElement = document.querySelector('.waveform');
    waveformElement.classList.remove('active');
    
    if (animationFrameId) {
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
    }
    
    // 重置所有波形條
    waveformBars.forEach(bar => {
        bar.style.height = '5px';
    });
}

// 添加在上面函數之後
function showSpeechRecognitionModal() {
    const modal = document.getElementById('speechRecognitionModal');
    const targetDisplay = modal.querySelector('.target-word');
    
    // 清除先前的結果
    const resultDisplay = modal.querySelector('.recognition-result');
    const scoreDisplay = modal.querySelector('.accuracy-score');
    const oldSyllableFeedback = modal.querySelector('.syllable-feedback');
    
    resultDisplay.textContent = '';
    scoreDisplay.textContent = '';
    scoreDisplay.className = 'accuracy-score';
    
    if (oldSyllableFeedback) {
        oldSyllableFeedback.remove();
    }
    
    // 設置目標文字
    let targetText = '';
    if (currentCard === 1) {
        // 單字練習
        targetText = vocabularyData[currentCategory][currentWordIndex].word;
    } else {
        // 例句練習
        if (vocabularyData[currentCategory][currentWordIndex].examples) {
            const exampleIndex = currentCard === 2 ? 0 : 1;
            if (vocabularyData[currentCategory][currentWordIndex].examples.length > exampleIndex) {
                targetText = vocabularyData[currentCategory][currentWordIndex].examples[exampleIndex].sentence;
            }
        } else if (currentCard === 2 && vocabularyData[currentCategory][currentWordIndex].example) {
            targetText = vocabularyData[currentCategory][currentWordIndex].example;
        }
    }
    
    targetDisplay.textContent = targetText;
    
    // 創建波形
    createWaveform();
    
    // 顯示模態框
    modal.style.display = 'block';
}

// 添加在 showSpeechRecognitionModal 函數之後
function startRecording(e) {
    e.preventDefault();
    
    if (!recognition) return;
    
    isRecording = true;
    const speechBtn = document.getElementById('recordButton');
    speechBtn.classList.add('recording');
    speechBtn.querySelector('.record-text').textContent = '正在聆聽...';
    
    // 開始波形動畫
    startWaveformAnimation();
    
    // 開始語音辨識
    try {
        recognition.start();
    } catch (error) {
        console.error('無法啟動語音辨識', error);
        isRecording = false;
        speechBtn.classList.remove('recording');
        speechBtn.querySelector('.record-text').textContent = '按住說話';
        stopWaveformAnimation();
    }
}

function stopRecording() {
    if (!isRecording) return;
    
    try {
        recognition.stop();
    } catch (error) {
        console.error('無法停止語音辨識', error);
    }
}

function createRipple(event) {
    const button = event.currentTarget;
    
    const circle = document.createElement('span');
    const diameter = Math.max(button.clientWidth, button.clientHeight);
    const radius = diameter / 2;
    
    const clientX = event.type.includes('touch') ? 
        event.touches[0].clientX : event.clientX;
    const clientY = event.type.includes('touch') ? 
        event.touches[0].clientY : event.clientY;
    
    const rect = button.getBoundingClientRect();
    const left = clientX - rect.left - radius;
    const top = clientY - rect.top - radius;
    
    circle.style.width = circle.style.height = `${diameter}px`;
    circle.style.left = `${left}px`;
    circle.style.top = `${top}px`;
    circle.classList.add('ripple');
    
    const ripple = button.getElementsByClassName('ripple')[0];
    
    if (ripple) {
        ripple.remove();
    }
    
    button.appendChild(circle);
}

        function initializeFlashcards() {
            updateCardVisibility();
            updateCardContent();
            updateCardIndicators();
            playCardAudio();
        }

        function changeCard(direction) {
    stopSpeaking();
    const flashcard = document.getElementById('flashcard');
    
    // 記錄要切換到的新卡片索引
    const totalCards = getTotalCards(currentCategory);
    const newCardIndex = (currentCard + direction + totalCards) % totalCards;
    
    console.log('切換卡片: 從', currentCard, '到', newCardIndex);
    
    // 添加翻轉動畫類
    flashcard.classList.remove('flip-right', 'flip-left');
    void flashcard.offsetWidth; // 強制重排，以便動畫正確播放
    flashcard.classList.add(direction > 0 ? 'flip-right' : 'flip-left');
    
    // 動畫完成後更新卡片
    setTimeout(() => {
        // 更新當前卡片索引
        currentCard = newCardIndex;
        
        // 更新卡片可見性狀態
        updateCardVisibility();
        
        // 更新卡片內容
        updateCardContent();
        
        // 更新指示器
        updateCardIndicators();
        
        // 重置翻譯容器
        document.querySelectorAll('.translation-container').forEach(container => {
            container.classList.remove('show');
        });
        
        // 移除翻轉動畫類，為下一次翻轉做準備
        flashcard.classList.remove('flip-right', 'flip-left');
        
        // 播放音頻
        setTimeout(() => {
            playCardAudio();
        }, 100);
    }, 300); // 等待卡片翻轉動畫完成
}

        function changeWord(direction) {
            stopSpeaking();
            const categoryWords = vocabularyData[currentCategory];
            const flashcard = document.getElementById('flashcard');
            flashcard.classList.remove('flip-right', 'flip-left');
            void flashcard.offsetWidth; // 觸發重排
            flashcard.classList.add(direction > 0 ? 'flip-right' : 'flip-left');

            setTimeout(() => {
        currentWordIndex = (currentWordIndex + direction + categoryWords.length) % categoryWords.length;
        currentCard = 0;
        updateCardVisibility();
        updateCardContent();
        updateCardIndicators();
        flashcard.classList.remove('flip-right', 'flip-left');
        
        // 添加這行重置翻譯狀態的代碼
        document.querySelectorAll('.translation-container').forEach(container => {
            container.classList.remove('show');
        });
        
        setTimeout(() => {
            playCardAudio();
        }, 100);
    }, 300);
}

        function updateCardVisibility() {
    console.log('更新卡片可見性: 當前卡片索引 =', currentCard);
    
    // 取得所有卡片
    const cards = document.querySelectorAll('.card');
    
    // 先將所有卡片設為隱藏（添加 back 類）
    cards.forEach(card => {
        card.classList.add('back');
    });
    
    // 再顯示當前卡片（移除 back 類）
    if (currentCard >= 0 && currentCard < cards.length) {
        cards[currentCard].classList.remove('back');
        console.log('顯示卡片:', currentCard);
    } else {
        console.error('無效的卡片索引:', currentCard);
    }
}

		function createTranslationContainer(translation) {
    const container = document.createElement('div');
    container.className = 'translation-container';
    container.innerHTML = `
        <div class="translation-hint">
            <svg class="translation-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
            </svg>
        </div>
        <div class="translation">${translation}</div>
    `;
    
    container.addEventListener('click', function() {
        this.classList.toggle('show');
    });
    
    // 阻止觸控事件的傳播
    container.addEventListener('touchstart', function(event) {
        event.stopPropagation();
    });
    
    container.addEventListener('touchmove', function(event) {
        event.stopPropagation();
    });
    
    container.addEventListener('touchend', function(event) {
        event.stopPropagation();
    });
    
    return container;
}

        function updateCardContent() {
    const currentWord = vocabularyData[currentCategory][currentWordIndex];
    const wordDisplay = document.getElementById('wordDisplay');
    const wordBack = document.getElementById('wordBack');
    const meaningDisplay = document.getElementById('meaningDisplay');
    const exampleDisplay = document.getElementById('exampleDisplay');
    const exampleDisplay2 = document.getElementById('exampleDisplay2');
    const exampleTextContainer = document.querySelector('#card3 .example-text');
    const exampleTextContainer2 = document.querySelector('#card4 .example-text');
    const imageContainer = document.getElementById('imageContainer');
    const imageContainer2 = document.getElementById('imageContainer2');

    // 先清空圖片容器
    imageContainer.innerHTML = '圖片預留區';
    imageContainer2.innerHTML = '圖片預留區';

    requestAnimationFrame(() => {
        // 更新基本內容
        wordDisplay.textContent = currentWord.word;
        wordBack.textContent = currentWord.word;
        meaningDisplay.textContent = currentWord.meaning;

        // 處理例句和翻譯
        if (currentWord.examples) {
            // 處理第一個例句
            if (currentWord.examples.length > 0) {
                const example1 = currentWord.examples[0];
                exampleDisplay.innerHTML = processExampleText(example1.sentence, currentWord.word);
                
                // 確保移除所有舊的翻譯容器
                const oldTranslation = exampleTextContainer.querySelector('.translation-container');
                if (oldTranslation) {
                    oldTranslation.remove();
                }
                
                // 創建並附加新的翻譯容器
                const translationContainer1 = createTranslationContainer(example1.translation);
                exampleTextContainer.appendChild(translationContainer1);

                if (example1.image) {
                    imageContainer.innerHTML = `<img src="${example1.image}" alt="${currentWord.word}" style="max-width: 100%; max-height: 100%; object-fit: contain;">`;
                }
            }

            // 處理第二個例句（如果存在）
            if (currentWord.examples.length > 1) {
                const example2 = currentWord.examples[1];
                exampleDisplay2.innerHTML = processExampleText(example2.sentence, currentWord.word);
                
                // 確保移除所有舊的翻譯容器
                const oldTranslation2 = exampleTextContainer2.querySelector('.translation-container');
                if (oldTranslation2) {
                    oldTranslation2.remove();
                }
                
                // 創建並附加新的翻譯容器
                const translationContainer2 = createTranslationContainer(example2.translation);
                exampleTextContainer2.appendChild(translationContainer2);

                if (example2.image) {
                    imageContainer2.innerHTML = `<img src="${example2.image}" alt="${currentWord.word}" style="max-width: 100%; max-height: 100%; object-fit: contain;">`;
                }
            }
        } else if (currentWord.example) {
            // 處理舊格式的例句
            exampleDisplay.innerHTML = processExampleText(currentWord.example, currentWord.word);
            
            // 確保移除所有舊的翻譯容器
            const oldTranslation = exampleTextContainer.querySelector('.translation-container');
            if (oldTranslation) {
                oldTranslation.remove();
            }
            
            // 創建並附加新的翻譯容器
            const translationContainer = createTranslationContainer(currentWord.translation);
            exampleTextContainer.appendChild(translationContainer);

            if (currentWord.image) {
                imageContainer.innerHTML = `<img src="${currentWord.image}" alt="${currentWord.word}" style="max-width: 100%; max-height: 100%; object-fit: contain;">`;
            }
        }

        // 調整卡片指示器
        updateCardIndicators();
        
        // 在所有內容更新完成後再添加語音按鈕
        setTimeout(() => {
            // 添加語音練習按鈕 (除了第一張卡片外)
            const cards = document.querySelectorAll('.card');
            cards.forEach((card, index) => {
                // 移除之前的按鈕 (如果有)
                const existingButton = card.querySelector('.speech-icon');
                if (existingButton) {
                    existingButton.remove();
                }
                
                // 不在第一張卡片添加按鈕
                if (index === 0) return;
                
                // 創建語音練習按鈕
                const speechButton = document.createElement('div');
                speechButton.className = 'speech-icon';
                speechButton.innerHTML = '🎤';
                speechButton.title = '練習發音';
                
                speechButton.addEventListener('click', (e) => {
                    e.stopPropagation(); // 防止觸發卡片翻轉
                    showSpeechRecognitionModal();
                });

                // 添加這些額外的事件監聽器
                speechButton.addEventListener('touchstart', (e) => {
                    e.stopPropagation();
                    e.preventDefault(); // 阻止默認行為
                }, { passive: false });

                speechButton.addEventListener('touchmove', (e) => {
                    e.stopPropagation();
                    e.preventDefault();
                }, { passive: false });

                speechButton.addEventListener('touchend', (e) => {
                    e.stopPropagation();
                    showSpeechRecognitionModal();
                }, { passive: false });
                
                // 將按鈕添加到卡片中 - 這行很重要，不能缺少
                card.appendChild(speechButton);
            });
            
            // 調整字體大小
            adjustWordDisplay();
        }, 50); // 短暫延遲以確保DOM已更新
    });
}

		function processExampleText(text, targetWord) {
    // 檢查目標詞是單詞還是片語
    const isPhrase = targetWord.includes(' ');
    
    if (isPhrase) {
        // 處理片語的情況
        return processExampleWithPhrase(text, targetWord);
    } else {
        // 處理單詞的情況 - 原有的邏輯
        const words = text.match(/[\w']+|[.,!?;]|\s+/g) || [];
        
        return words.map((word, index) => {
            const cleanWord = word.trim().toLowerCase().replace(/[.,!?;]$/, '');
            const isTargetWord = cleanWord === targetWord.toLowerCase();
            const isPunctuation = /^[.,!?;]$/.test(word);
            const isSpace = /^\s+$/.test(word);
            
            if (isSpace) {
                return ' ';
            }
            
            return `<span 
                data-index="${index}" 
                class="${isTargetWord ? 'highlight-word' : ''}"
                ${isPunctuation ? 'style="margin-left: -2px;"' : ''}
            >${word}</span>`;
        }).join('');
    }
}

		function processExampleWithPhrase(text, targetPhrase) {
    // 創建一個函數來處理片語的變形
    function getPhraseVariations(phrase) {
        let variations = [phrase.toLowerCase()];
        let originalPhrase = phrase.toLowerCase();
        let words = originalPhrase.split(/\s+/);
        
        // 處理冠詞變化 (a/the)
        if (originalPhrase.includes("a/the")) {
            const withA = originalPhrase.replace("a/the", "a");
            const withThe = originalPhrase.replace("a/the", "the");
            variations.push(withA, withThe);
            // 添加不含冠詞的版本，因為例句可能省略冠詞
            variations.push(originalPhrase.replace("a/the ", ""));
        }
        
        // 處理動詞變化
        if (words[0] === 'be') {
            // be 動詞的變形: am, is, are, was, were, been, being
            const beVariations = ['am', 'is', 'are', 'was', 'were', 'been', 'being'];
            beVariations.forEach(verb => {
                variations.push(originalPhrase.replace(/^be\s/, verb + ' '));
            });
        } else if (words[0] === 'have') {
            // have 動詞的變形: has, had, having
            const haveVariations = ['has', 'had', 'having'];
            haveVariations.forEach(verb => {
                variations.push(originalPhrase.replace(/^have\s/, verb + ' '));
            });
        } else if (words[0] === 'give' || words[0] === 'go' || words[0] === 'make') {
            // 其他動詞的常見變形: 第三人稱單數、過去式、現在分詞、過去分詞
            const verbForms = {
                'give': ['gives', 'gave', 'giving', 'given'],
                'go': ['goes', 'went', 'going', 'gone'],
                'make': ['makes', 'made', 'making']
            };
            
            if (verbForms[words[0]]) {
                verbForms[words[0]].forEach(verb => {
                    variations.push(originalPhrase.replace(new RegExp(`^${words[0]}\\s`), verb + ' '));
                });
            }
        }
        
        // 處理代詞變化 (one's)
        if (originalPhrase.includes("one's")) {
            const pronouns = ['my', 'your', 'his', 'her', 'its', 'our', 'their'];
            pronouns.forEach(pronoun => {
                variations.push(originalPhrase.replace("one's", pronoun));
            });
        }
        
        // 處理 sth./sb. 變化
        if (originalPhrase.includes("sth.")) {
            // 添加不帶 sth. 的基本形式，因為實際例句中會用具體名詞替換
            variations.push(originalPhrase.replace(" sth.", ""));
            // 還可能縮寫為 something
            variations.push(originalPhrase.replace("sth.", "something"));
            // 或是具體名詞
            variations.push(originalPhrase.replace("sth.", ""));
        }
        
        // 處理 "all the time" 這類特殊片語
        if (originalPhrase === "all the time") {
            variations.push("all the time");
            variations.push("all times");
        }
        
        return variations;
    }
    
    // 生成可能的片語變形
    const phraseVariations = getPhraseVariations(targetPhrase);
    const lowerText = text.toLowerCase();
    
    // 尋找最佳匹配
    let bestMatch = null;
    let bestMatchIndex = -1;
    let bestMatchLength = 0;
    
    // 方法1: 嘗試完整匹配任一變形
    for (const variation of phraseVariations) {
        const index = lowerText.indexOf(variation);
        if (index !== -1 && variation.length > bestMatchLength) {
            bestMatch = variation;
            bestMatchIndex = index;
            bestMatchLength = variation.length;
        }
    }
    
    // 方法2: 如果未找到完整匹配，嘗試使用正則表達式進行更靈活的匹配
    if (bestMatchIndex === -1) {
        const originalWords = targetPhrase.toLowerCase().split(/\s+/);
        
        // 處理 "all the time" 特殊情況
        if (targetPhrase.toLowerCase() === "all the time") {
            const allTimeRegex = /\ball\s+the\s+time\b/i;
            const match = allTimeRegex.exec(text);
            if (match) {
                bestMatch = match[0];
                bestMatchIndex = match.index;
                bestMatchLength = match[0].length;
            }
        }
        
        // 處理 "make a/the difference" 特殊情況
        if (targetPhrase.toLowerCase().includes("make a/the difference")) {
            const differenceRegex = /\bmake\s+a\s+difference\b|\bmake\s+the\s+difference\b|\bmakes?\s+a\s+difference\b|\bmakes?\s+the\s+difference\b|\bmade\s+a\s+difference\b|\bmade\s+the\s+difference\b/i;
            const match = differenceRegex.exec(text);
            if (match) {
                bestMatch = match[0];
                bestMatchIndex = match.index;
                bestMatchLength = match[0].length;
            }
        }
        
        // 處理 "be in the same boat" 特殊情況
        if (targetPhrase.toLowerCase().includes("be in the same boat")) {
            const boatRegex = /\b(?:am|is|are|was|were|been|being)\s+in\s+the\s+same\s+boat\b/i;
            const match = boatRegex.exec(text);
            if (match) {
                bestMatch = match[0];
                bestMatchIndex = match.index;
                bestMatchLength = match[0].length;
            }
        }
        
        // 處理 "go for sth." 特殊情況
        if (targetPhrase.toLowerCase().includes("go for")) {
            const goForRegex = /\b(?:go|goes|went|going|gone)\s+for\b/i;
            const match = goForRegex.exec(text);
            if (match) {
                bestMatch = match[0];
                bestMatchIndex = match.index;
                bestMatchLength = match[0].length;
            }
        }
        
        // 處理 "have one's back" 特殊情況
        if (targetPhrase.toLowerCase().includes("have one's back")) {
            const haveBackRegex = /\b(?:have|has|had|having)\s+(?:my|your|his|her|its|our|their)\s+back\b/i;
            const match = haveBackRegex.exec(text);
            if (match) {
                bestMatch = match[0];
                bestMatchIndex = match.index;
                bestMatchLength = match[0].length;
            }
        }
        
        // 處理短語動詞可能分離的情況
        if (bestMatchIndex === -1 && originalWords.length >= 2 && 
            (originalWords[originalWords.length-1] === 'up' || 
             originalWords[originalWords.length-1] === 'down' ||
             originalWords[originalWords.length-1] === 'in' ||
             originalWords[originalWords.length-1] === 'out' ||
             originalWords[originalWords.length-1] === 'off' ||
             originalWords[originalWords.length-1] === 'on')) {
            
            const verb = originalWords[0];
            const particle = originalWords[originalWords.length-1];
            
            // 檢查動詞和介詞是否都存在於文本中
            const verbIndex = lowerText.indexOf(verb);
            const particleIndex = lowerText.indexOf(particle, verbIndex + 1);
            
            if (verbIndex !== -1 && particleIndex !== -1 && 
                particleIndex - verbIndex < 30) { // 限制動詞和介詞之間的距離
                
                // 嘗試識別分離的短語動詞
                return processTextWithSeparatedPhraseVerb(text, verb, particle, verbIndex, particleIndex);
            }
        }
    }
    
    // 如果仍未找到匹配，嘗試更寬鬆的識別方式（關鍵詞匹配）
    if (bestMatchIndex === -1) {
        return processWithKeywordHighlighting(text, targetPhrase);
    }
    
    // 當找到完整匹配時，準備高亮顯示
    const actualPhrase = text.substring(bestMatchIndex, bestMatchIndex + bestMatchLength);
    
    // 將例句分為三部分
    const beforePhrase = text.substring(0, bestMatchIndex);
    const afterPhrase = text.substring(bestMatchIndex + bestMatchLength);
    
    // 處理片語前的部分
    let beforeHtml = '';
    if (beforePhrase) {
        const beforeWords = beforePhrase.match(/[\w']+|[.,!?;]|\s+/g) || [];
        beforeHtml = beforeWords.map((word, index) => {
            const isSpace = /^\s+$/.test(word);
            if (isSpace) return ' ';
            return `<span data-index="${index}">${word}</span>`;
        }).join('');
    }
    
    // 處理片語本身 - 保持作為一個整體
    const phraseHtml = `<span class="highlight-word" style="font-weight: 700;">${actualPhrase}</span>`;
    
    // 處理片語後的部分
    let afterHtml = '';
    if (afterPhrase) {
        const afterWords = afterPhrase.match(/[\w']+|[.,!?;]|\s+/g) || [];
        
        afterHtml = afterWords.map((word, index) => {
            const isSpace = /^\s+$/.test(word);
            if (isSpace) return ' ';
            return `<span data-index="${index + beforePhrase.split(/\s+/).length + actualPhrase.split(/\s+/).length}">${word}</span>`;
        }).join('');
    }
    
    return beforeHtml + phraseHtml + afterHtml;
}

// 處理分離的短語動詞
function processTextWithSeparatedPhraseVerb(text, verb, particle, verbIndex, particleIndex) {
    const words = text.match(/[\w']+|[.,!?;]|\s+/g) || [];
    let result = '';
    let currentIndex = 0;
    let verbHighlighted = false;
    let particleHighlighted = false;
    
    words.forEach((word, index) => {
        const cleanWord = word.trim().toLowerCase().replace(/[.,!?;]$/, '');
        const isPunctuation = /^[.,!?;]$/.test(word);
        const isSpace = /^\s+$/.test(word);
        
        if (isSpace) {
            result += ' ';
            return;
        }
        
        // 更精確的匹配邏輯
        const wordStartIndex = text.toLowerCase().indexOf(cleanWord, currentIndex);
        const isVerb = !verbHighlighted && 
                       cleanWord === verb.toLowerCase() && 
                       Math.abs(wordStartIndex - verbIndex) < 3;
        
        const isParticle = !particleHighlighted && 
                         cleanWord === particle.toLowerCase() && 
                         Math.abs(wordStartIndex - particleIndex) < 3;
        
        if (isVerb) {
            result += `<span data-index="${index}" class="highlight-word">${word}</span>`;
            verbHighlighted = true;
        } else if (isParticle) {
            result += `<span data-index="${index}" class="highlight-word">${word}</span>`;
            particleHighlighted = true;
        } else {
            result += `<span data-index="${index}">${word}</span>`;
        }
        
        if (!isSpace) {
            currentIndex = wordStartIndex + cleanWord.length;
        }
    });
    
    return result;
}

// 處理關鍵詞高亮（當找不到完整匹配時）
function processWithKeywordHighlighting(text, targetPhrase) {
    const words = text.match(/[\w']+|[.,!?;]|\s+/g) || [];
    let phraseWords = targetPhrase.toLowerCase()
                      .replace(/a\/the/g, '') // 移除 a/the
                      .replace(/sth\./g, '')  // 移除 sth.
                      .replace(/one's/g, '')  // 移除 one's
                      .replace(/\s+/g, ' ')   // 標準化空格
                      .trim()
                      .split(/\s+/)
                      .filter(word => word.length > 0);
    
    // 為每個片語定義關鍵詞
    const keywordsMap = {
        "be in the same boat": ["boat", "same"],
        "make a/the difference": ["difference"],
        "go for sth": ["went", "for"],
        "give up": ["give", "gives", "giving", "gave", "up"],
        "have one's back": ["back"],
        "all the time": ["time"]
    };
    
    // 查找匹配的關鍵詞
    let keywordsToHighlight = [];
    for (const [phrase, keywords] of Object.entries(keywordsMap)) {
        if (targetPhrase.toLowerCase().includes(phrase) || 
            phrase.includes(targetPhrase.toLowerCase())) {
            keywordsToHighlight = keywords;
            break;
        }
    }
    
    // 如果沒有找到特定的關鍵詞，使用過濾後的片語詞
    if (keywordsToHighlight.length === 0) {
        // 過濾常見的無意義詞（除非它們是片語的關鍵部分）
        keywordsToHighlight = phraseWords.filter(word => 
            word.length > 3 || 
            ['up', 'in', 'on', 'for', 'the', 'off', 'out', 'down'].includes(word)
        );
    }
    
    return words.map((word, index) => {
        const cleanWord = word.trim().toLowerCase().replace(/[.,!?;]$/, '');
        const isPunctuation = /^[.,!?;]$/.test(word);
        const isSpace = /^\s+$/.test(word);
        
        if (isSpace) return ' ';
        
        // 檢查是否是片語中的關鍵詞
        const isKeyword = keywordsToHighlight.includes(cleanWord);
        
        return `<span 
            data-index="${index}" 
            class="${isKeyword ? 'highlight-word' : ''}"
            ${isPunctuation ? 'style="margin-left: -2px;"' : ''}
        >${word}</span>`;
    }).join('');
}

        function updateCardIndicators() {
    const indicators = document.querySelectorAll('.indicator');
    const totalCards = getTotalCards(currentCategory);
    
    // 更新指示器的顯示
    indicators.forEach((indicator, index) => {
        if (index < totalCards) {
            indicator.style.display = 'block';
            indicator.classList.toggle('active', index === currentCard);
        } else {
            indicator.style.display = 'none';
        }
    });
}

        async function playCardAudio() {
    const currentWord = vocabularyData[currentCategory][currentWordIndex];
    const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
    
    // 獲取最佳語音設置
    const voiceSettings = getVoiceSettings();

    if (currentCard === 0) {
        return playAudio();
    } else if (currentCard === 1) {
        return speak(currentWord.word, voiceSettings);
    } else if (currentCard === 2 || currentCard === 3) {
        // 確定當前顯示的是哪個例句和相應的DOM元素
        const exampleDisplay = currentCard === 2 ? 
            document.getElementById('exampleDisplay') : 
            document.getElementById('exampleDisplay2');
        
        let exampleText = '';
        
        // 判斷是使用新格式還是舊格式來獲取例句文本
        if (currentWord.examples && currentWord.examples.length > 0) {
            const exampleIndex = currentCard === 2 ? 0 : 1;
            if (currentWord.examples.length > exampleIndex) {
                exampleText = currentWord.examples[exampleIndex].sentence;
            }
        } else if (currentCard === 2 && currentWord.example) {
            exampleText = currentWord.example;
        }
        
        if (!exampleText) return Promise.resolve();

        return new Promise((resolve) => {
            // 創建語音實例
            const utterance = new SpeechSynthesisUtterance(exampleText);
            Object.assign(utterance, voiceSettings);

            // 調整語音速率 - 放慢速度以便跟上高亮
            utterance.rate = isIOS ? 0.75 : 0.7; // 比之前更慢
            
            // iOS 特定優化
            if (isIOS) {
                utterance.pitch = 1.1;
            }

            let lastHighlightedIndex = -1;
            let pendingHighlight = null;

            utterance.onboundary = function(event) {
                if (event.name === 'word') {
                    // 取消上一個待定高亮
                    if (pendingHighlight) {
                        clearTimeout(pendingHighlight);
                    }
                    
                    // 延遲高亮顯示以減少偏差
                    pendingHighlight = setTimeout(() => {
                        requestAnimationFrame(() => {
                            // 清除上一個高亮
                            if (lastHighlightedIndex >= 0) {
                                const prevWord = exampleDisplay.querySelector(`span[data-index="${lastHighlightedIndex}"]`);
                                if (prevWord && !prevWord.classList.contains('highlight-word')) {
                                    prevWord.classList.remove('highlight');
                                }
                            }

                            // 使用更準確的字符匹配算法
                            const spans = exampleDisplay.querySelectorAll('span');
                            let bestSpan = null;
                            let minDistance = Infinity;
                            let charCount = 0;
                            
                            // 遍歷所有 span，找到最接近當前朗讀位置的單詞
                            for (let i = 0; i < spans.length; i++) {
                                const span = spans[i];
                                const spanLength = span.textContent.length;
                                
                                // 計算開始和結束位置
                                const startDist = Math.abs(charCount - event.charIndex);
                                const endDist = Math.abs(charCount + spanLength - event.charIndex);
                                
                                // 如果這個 span 包含當前朗讀位置，或者最接近
                                if (startDist < minDistance || endDist < minDistance) {
                                    minDistance = Math.min(startDist, endDist);
                                    bestSpan = span;
                                }
                                
                                charCount += spanLength + 1; // +1 為空格
                            }

                            if (bestSpan) {
                                bestSpan.classList.add('highlight');
                                lastHighlightedIndex = bestSpan.dataset.index;
                                
                                // 平滑滾動到當前單字
                                if (exampleDisplay.scrollHeight > exampleDisplay.clientHeight) {
                                    bestSpan.scrollIntoView({
                                        behavior: 'smooth',
                                        block: 'center',
                                        inline: 'nearest'
                                    });
                                }
                            }
                        });
                    }, 50); // 50ms 的延遲，可以根據需要調整
                }
            };

            utterance.onend = function() {
                // 清除所有臨時高亮，但保留目標單字的特殊樣式
                exampleDisplay.querySelectorAll('span').forEach(span => {
                    if (!span.classList.contains('highlight-word')) {
                        span.classList.remove('highlight');
                    }
                });
                resolve();
            };

            utterance.onerror = function(event) {
                console.error('Speech synthesis error:', event);
                exampleDisplay.querySelectorAll('span:not(.highlight-word)').forEach(span => {
                    span.classList.remove('highlight');
                });
                resolve();
            };

            // 播放語音
            speechSynthesis.speak(utterance);
        });
    }
    
    return Promise.resolve();
}

        function getVoiceSettings() {
            const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
            const voices = speechSynthesis.getVoices();
            
            // 選擇最佳語音
            const selectedVoice = isIOS ? 
                voices.find(voice => 
                    voice.lang === 'en-US' && 
                    (voice.name.includes('Samantha') || voice.name.includes('Karen'))
                ) || voices.find(voice => 
                    voice.lang === 'en-US'
                ) :
                voices.find(voice => 
                    voice.lang === 'en-US' && 
                    voice.name.includes('Google')
                ) || voices.find(voice => 
                    voice.lang === 'en-US'
                );

            return {
                voice: selectedVoice,
                lang: 'en-US',
                pitch: isIOS ? 1.1 : 1.0,
                rate: isIOS ? 0.9 : 0.8
            };
        }

        async function playAudio() {
    const currentWord = vocabularyData[currentCategory][currentWordIndex];
    const wordDisplay = document.getElementById('wordDisplay');
    
    // 檢測是否為 iOS 設備
    const isIOS = /iPad|iPhone|iPod/.test(navigator.userAgent) && !window.MSStream;
    
    // 獲取並設置預設語音
    const voices = speechSynthesis.getVoices();
    const selectedVoice = isIOS ? 
        voices.find(voice => 
            voice.lang === 'en-US' && 
            (voice.name.includes('Samantha') || voice.name.includes('Karen'))
        ) || voices.find(voice => 
            voice.lang === 'en-US'
        ) :
        voices.find(voice => 
            voice.lang === 'en-US' && 
            voice.name.includes('Google')
        ) || voices.find(voice => 
            voice.lang === 'en-US'
        );

    // 基本語音設置
    const voiceSettings = {
        voice: selectedVoice,
        lang: 'en-US',
        pitch: isIOS ? 1.1 : 1.0,
    };
    
    // 先顯示完整單字並正常速度發音
    wordDisplay.textContent = currentWord.word;
    await speak(currentWord.word, { 
        ...voiceSettings, 
        rate: isIOS ? 0.9 : 0.8 
    });

    // 如果是片語類別，直接返回，不進行音節朗讀
    // 如果是片語類別
    if (currentCategory === 'idioms') {
        // 建立片語的音節容器
        wordDisplay.innerHTML = `
            <div class="syllables-container" style="
                display: flex;
                justify-content: center;
                align-items: center;
                flex-wrap: nowrap;
                width: 100%;
                padding: 0 10px;
                gap: 2px;
                height: 100%;
            ">
            </div>`;
        const container = wordDisplay.querySelector('.syllables-container');
        
        // 將片語分割成單字
        const words = currentWord.word.split(' ');
        words.forEach((word, index) => {
            container.innerHTML += `
                <span class="syllable" style="
                    display: inline-block;
                    white-space: nowrap;
                    text-align: center;
                    min-width: min-content;
                    flex: 0 1 auto;
                ">${word}</span>`;
            if (index < words.length - 1) {
                container.innerHTML += `
                    <span class="syllable-separator" style="
                        margin: 0 1px;
                        color: #666;
                        flex-shrink: 1;
                    "> </span>`;
            }
        });

        adjustFontSize(container);
        
        const syllables = container.querySelectorAll('.syllable');
        const baseDelay = isIOS ? 500 : 400;
        
        // 播放慢速版本並同步 highlight
        const slowSpeechPromise = new Promise(resolve => {
            const utterance = new SpeechSynthesisUtterance(currentWord.word);
            Object.assign(utterance, {
                ...voiceSettings,
                rate: isIOS ? 0.25 : 0.3,
                pitch: isIOS ? 1.1 : 1.0
            });
            utterance.onend = resolve;
            
            setTimeout(() => {
                speechSynthesis.speak(utterance);
            }, 100);
        });

        // 處理視覺高亮效果
        for (let i = 0; i < words.length; i++) {
            syllables.forEach((s, index) => {
                s.classList.toggle('highlight', index === i);
            });
            await new Promise(resolve => setTimeout(resolve, baseDelay));
        }

        await slowSpeechPromise;
        
        // 最後正常速度發音
        wordDisplay.textContent = currentWord.word;
        await speak(currentWord.word, { 
            ...voiceSettings, 
            rate: isIOS ? 0.9 : 0.8 
        });
        return;
    }
    
    // 以下是非片語類別的音節處理
    wordDisplay.innerHTML = `
        <div class="syllables-container" style="
            display: flex;
            justify-content: center;
            align-items: center;
            flex-wrap: nowrap;
            width: 100%;
            padding: 0 10px;
            gap: 2px;
            height: 100%;
        ">
        </div>`;
    const container = wordDisplay.querySelector('.syllables-container');
    
    // 添加音節到容器
    currentWord.syllables.forEach((syllable, index) => {
        container.innerHTML += `
            <span class="syllable" style="
                display: inline-block;
                white-space: nowrap;
                text-align: center;
                min-width: min-content;
                flex: 0 1 auto;
            ">${syllable}</span>`;
        if (index < currentWord.syllables.length - 1) {
            container.innerHTML += `
                <span class="syllable-separator" style="
                    margin: 0 1px;
                    color: #666;
                    flex-shrink: 1;
                ">．</span>`;
        }
    });

    // 調整字體大小
    adjustFontSize(container);
    
    const syllables = container.querySelectorAll('.syllable');
    
    // 計算基礎延遲時間（針對 iOS 優化）
    const baseDelay = isIOS ? 500 : 400;
    const syllableDurations = currentWord.syllables.map(syllable => 
        Math.max(baseDelay, Math.round((syllable.length / currentWord.word.length) * baseDelay * 2))
    );
    
    // 計算總持續時間
    const totalDuration = syllableDurations.reduce((sum, duration) => sum + duration, 0);
    
    // 設置語音速率（保留 iOS 的優化）
    const rateAdjustment = isIOS ? 0.25 : 0.3;
    
    // 同步播放慢速語音和顯示音節
    const slowSpeechPromise = new Promise(resolve => {
        const utterance = new SpeechSynthesisUtterance(currentWord.word);
        Object.assign(utterance, {
            ...voiceSettings,
            rate: rateAdjustment,
            pitch: isIOS ? 1.1 : 1.0
        });
        utterance.onend = resolve;
        
        setTimeout(() => {
            speechSynthesis.speak(utterance);
        }, 100);
    });

    // 處理視覺高亮效果
    let currentDelay = 0;
    for (let i = 0; i < currentWord.syllables.length; i++) {
        syllables.forEach((s, index) => {
            s.classList.toggle('highlight', index === i);
        });
        
        await new Promise(resolve => setTimeout(resolve, syllableDurations[i]));
        currentDelay += syllableDurations[i];
    }

    await slowSpeechPromise;
    
    // 最後正常速度發音（保留 iOS 的優化）
    wordDisplay.textContent = currentWord.word;
    await speak(currentWord.word, { 
        ...voiceSettings, 
        rate: isIOS ? 0.9 : 0.8,
        pitch: isIOS ? 1.1 : 1.0 
    });
}
        function adjustFontSize(container) {
            const maxFontSize = 36;
            const minFontSize = 16;
            let fontSize = maxFontSize;
            const syllables = container.querySelectorAll('.syllable');
            
            // 設置容器基本樣式
            container.style.display = 'flex';
            container.style.justifyContent = 'center';
            container.style.alignItems = 'center';
            container.style.width = '100%';
            container.style.height = '100%';
            container.style.padding = '0 10px';
            container.style.boxSizing = 'border-box';
            container.style.margin = '0';
            container.style.overflow = 'hidden';
            
            // 初始字體大小
            container.style.fontSize = `${fontSize}px`;
            
            // 循環檢查並調整字體大小
            while (fontSize > minFontSize && 
                   (container.scrollWidth > container.offsetWidth || 
                    container.scrollHeight > container.offsetHeight)) {
                fontSize -= 1;
                container.style.fontSize = `${fontSize}px`;
            }
            
            // 調整容器內的音節和分隔符樣式
            syllables.forEach(syllable => {
                syllable.style.display = 'inline-block';
                syllable.style.padding = '0 2px';
                syllable.style.whiteSpace = 'nowrap';
                syllable.style.textAlign = 'center';
            });

            const separators = container.querySelectorAll('.syllable-separator');
            separators.forEach(separator => {
                separator.style.padding = '0';
                separator.style.margin = '0 1px';
            });

            // 如果還是太大，進一步調整
            if (container.scrollWidth > container.offsetWidth) {
                separators.forEach(separator => {
                    separator.style.margin = '0';
                });
                container.style.letterSpacing = '-0.5px';
            }
        }

        async function speak(text, options = {}) {
            return new Promise((resolve, reject) => {
                const utterance = new SpeechSynthesisUtterance(text);
                Object.assign(utterance, getVoiceSettings(), options);
                utterance.onend = resolve;
                utterance.onerror = reject;
                speechSynthesis.speak(utterance);
            });
        }

        function stopSpeaking() {
            window.speechSynthesis.cancel();
        }

        function showWordList() {
            const modal = document.getElementById('wordListModal');
            const wordList = document.getElementById('wordListItems');
            wordList.innerHTML = '';
            vocabularyData[currentCategory].forEach((word, index) => {
                const li = document.createElement('li');
                li.textContent = word.word;
                li.onclick = () => {
                    stopSpeaking();
                    currentWordIndex = index;
                    currentCard = 0;
                    updateCardVisibility();
                    updateCardContent();
                    updateCardIndicators();
                    modal.style.display = 'none';
                    setTimeout(() => {
                        playCardAudio();
                    }, 100);
                };
                wordList.appendChild(li);
            });
            modal.style.display = 'block';
        }

        // 添加類別切換功能
        document.addEventListener('DOMContentLoaded', () => {
    const categoryButtons = document.querySelectorAll('.category-btn');
    categoryButtons.forEach(button => {
        button.addEventListener('click', () => {
            stopSpeaking();
            
            categoryButtons.forEach(btn => btn.classList.remove('active'));
            button.classList.add('active');
            
            const newCategory = button.dataset.category;
            currentCategory = newCategory;
            currentWordIndex = 0;
            currentCard = 0;
            
            // 確保切換到認知類別時，如果當前在第三張卡片，要重置到第一張
            if (currentCategory === 'recognition' && currentCard >= 2) {
                currentCard = 0;
            }
            
            updateCardVisibility();
            updateCardContent();
            updateCardIndicators();
            
            setTimeout(() => {
                playCardAudio();
            }, 100);
            // 添加初始字體大小調整
    adjustWordDisplay();
        });
    });
});

        document.getElementById('prevWord').onclick = () => changeWord(-1);
        document.getElementById('nextWord').onclick = () => changeWord(1);
        document.getElementById('wordListBtn').onclick = showWordList;

        document.querySelector('.close').onclick = function() {
            document.getElementById('wordListModal').style.display = 'none';
        }

        let touchStartX = 0;
        let touchEndX = 0;

        function handleTouchStart(e) {
    // 檢查是否點擊在翻譯容器上
    if (e.target.closest('.translation-container')) {
        return;  // 如果是點擊翻譯容器，直接返回不處理
    }
    touchStartX = e.touches[0].clientX;
}

function handleTouchMove(e) {
    // 檢查是否點擊在翻譯容器上
    if (e.target.closest('.translation-container')) {
        return;  // 如果是點擊翻譯容器，直接返回不處理
    }
    touchEndX = e.touches[0].clientX;
}

function handleTouchEnd(e) {
    // 檢查是否點擊在翻譯容器上
    if (e.target.closest('.translation-container')) {
        return;  // 如果是點擊翻譯容器，直接返回不處理
    }

    const totalCards = getTotalCards(currentCategory);
    if (touchStartX - touchEndX > 50) {
        if (currentCard < totalCards - 1) {
            changeCard(1);
        }
    }
    if (touchEndX - touchStartX > 50) {
        if (currentCard > 0) {
            changeCard(-1);
        }
    }
    touchStartX = 0;
    touchEndX = 0;
}

        document.addEventListener('DOMContentLoaded', (event) => {
            const flashcard = document.getElementById('flashcard');
            flashcard.addEventListener('touchstart', handleTouchStart, false);
            flashcard.addEventListener('touchmove', handleTouchMove, false);
            flashcard.addEventListener('touchend', handleTouchEnd, false);

            const indicators = document.querySelectorAll('.indicator');
            indicators.forEach((indicator, index) => {
                indicator.addEventListener('click', () => {
                    if (index !== currentCard) {
                        changeCard(index - currentCard);
                    }
                });
            });
        });
function adjustWordDisplay() {
    const wordElements = document.querySelectorAll('.word');
    
    wordElements.forEach(element => {
        // 重置任何之前的轉換
        element.style.transform = 'scale(1)';
        element.style.fontSize = ''; // 重置字體大小
        
        const maxWidth = element.parentElement.offsetWidth - 40; // 考慮 padding
        const maxHeight = element.parentElement.offsetHeight / 3; // 預留空間給其他元素
        
        // 檢查是否溢出
        const isOverflowing = element.scrollWidth > maxWidth || 
                            element.scrollHeight > maxHeight;
        
        if (isOverflowing) {
            // 計算縮放比例
            const widthRatio = maxWidth / element.scrollWidth;
            const heightRatio = maxHeight / element.scrollHeight;
            const scale = Math.min(widthRatio, heightRatio, 1) * 0.95;
            
            // 應用縮放
            element.style.transform = `scale(${scale})`;
            element.classList.add('auto-scale');
            
            // 調整容器高度以確保居中
            element.style.height = `${maxHeight}px`;
            element.style.display = 'flex';
            element.style.alignItems = 'center';
            element.style.justifyContent = 'center';
        }
    });
}
   function showGuide() {
    document.getElementById('guideModal').style.display = 'block';
    document.body.style.overflow = 'hidden';
}

function hideGuide() {
    document.getElementById('guideModal').style.display = 'none';
    document.body.style.overflow = 'auto';
}

// 點擊背景關閉導覽
window.onclick = function(event) {
    const modal = document.getElementById('guideModal');
    if (event.target == modal) {
        hideGuide();
    }
}

	function initializeSpeech() {
    // 載入語音合成引擎
    if (window.speechSynthesis) {
        // 確保 getVoices 函數已載入聲音
        if (speechSynthesis.getVoices().length === 0) {
            speechSynthesis.onvoiceschanged = function() {
                console.log('語音合成引擎已初始化');
            };
        }
    } else {
        console.warn('瀏覽器不支援語音合成');
    }
    
    // 檢查麥克風
    checkMicrophoneAccess();
}

// 檢查麥克風權限
function checkMicrophoneAccess() {
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
        console.error('瀏覽器不支援 getUserMedia API');
        return;
    }
    
    console.log('檢查麥克風權限...');
    navigator.mediaDevices.getUserMedia({ audio: true })
        .then(stream => {
            console.log('成功獲取麥克風權限');
            // 釋放流
            stream.getTracks().forEach(track => track.stop());
            // 初始化語音辨識
            if (initializeSpeechRecognition()) {
                console.log('語音辨識已初始化');
            }
        })
        .catch(err => {
            console.error('無法獲取麥克風權限:', err);
        });
}

function initializeSpeechRecognition() {
    // 檢查瀏覽器是否支援語音辨識
    window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    
    if (!window.SpeechRecognition) {
        console.error('您的瀏覽器不支援語音辨識功能');
        return false;
    }
    
    try {
        window.recognition = new SpeechRecognition();
        window.recognition.lang = 'en-US';
        window.recognition.interimResults = false;
        window.recognition.maxAlternatives = 1;
        
        // 設置辨識結果處理函數
        window.recognition.onresult = handleSpeechResult;
        window.recognition.onerror = handleSpeechError;
        window.recognition.onend = handleSpeechEnd;
        
        // 初始化音頻分析器 (用於波形顯示)
        initializeAudioAnalyser();
        
        // 設置全局狀態變量
        window.isRecording = false;
        window.isRecordingActive = false;
        
        return true;
    } catch (error) {
        console.error('初始化語音辨識時發生錯誤:', error);
        return false;
    }
}

function initializeAudioAnalyser() {
    try {
        window.audioContext = new (window.AudioContext || window.webkitAudioContext)();
        window.analyser = window.audioContext.createAnalyser();
        window.analyser.fftSize = 256;
        console.log('音頻分析器初始化成功');
    } catch (error) {
        console.error('無法初始化音頻分析器', error);
    }
}

function createWaveform() {
    console.log('創建波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (!waveformElement) {
        console.error('找不到波形容器');
        return;
    }
    
    waveformElement.innerHTML = '';
    window.waveformBars = [];
    
    const barCount = 30;
    
    for (let i = 0; i < barCount; i++) {
        const bar = document.createElement('div');
        bar.className = 'wave-bar';
        bar.style.height = '5px'; // 初始高度
        waveformElement.appendChild(bar);
        window.waveformBars.push(bar);
    }
    
    console.log(`已創建 ${barCount} 個波形條`);
}

function startWaveformAnimation() {
    console.log('開始波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (!waveformElement) {
        console.error('找不到波形容器');
        return;
    }
    
    waveformElement.classList.add('active');
    
    function updateWaveform() {
        if (!window.isRecording) {
            console.log('錄音已停止，不再更新波形');
            return;
        }
        
        // 模擬麥克風輸入
        if (window.waveformBars && window.waveformBars.length > 0) {
            for (let i = 0; i < window.waveformBars.length; i++) {
                const height = Math.floor(Math.random() * 25) + 5;
                window.waveformBars[i].style.height = `${height}px`;
            }
        }
        
        window.animationFrameId = requestAnimationFrame(updateWaveform);
    }
    
    updateWaveform();
    console.log('波形動畫已啟動');
}

function stopWaveformAnimation() {
    console.log('停止波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (waveformElement) {
        waveformElement.classList.remove('active');
    }
    
    if (window.animationFrameId) {
        cancelAnimationFrame(window.animationFrameId);
        window.animationFrameId = null;
    }
    
    // 重置所有波形條
    if (window.waveformBars) {
        window.waveformBars.forEach(bar => {
            if (bar) bar.style.height = '5px';
        });
    }
}

window.onload = function() {
    try {
        console.log('頁面載入完成');
        initializeFlashcards();
        initializeSpeech();
        
        // 設置預設分類按鈕
        const categoryButtons = document.querySelectorAll('.category-btn');
        categoryButtons[0].classList.add('active');
        
        // 初始化指示器
        updateCardIndicators();
        
        // 添加觸控事件監聽
        const flashcard = document.getElementById('flashcard');
        flashcard.addEventListener('touchstart', handleTouchStart, false);
        flashcard.addEventListener('touchmove', handleTouchMove, false);
        flashcard.addEventListener('touchend', handleTouchEnd, false);
        
        // 添加指示器點擊事件
        const indicators = document.querySelectorAll('.indicator');
        indicators.forEach((indicator, index) => {
            indicator.addEventListener('click', () => {
                if (index !== currentCard) {
                    changeCard(index - currentCard);
                }
            });
        });
        
        // 初始化語音練習按鈕
        setupSpeechRecognitionButton();
        console.log('語音按鈕已設置');
        
        // 設置語音模態框關閉按鈕
        setupModalCloseButton();
        
    } catch (error) {
        console.error('初始化錯誤:', error);
        alert('頁面初始化出錯: ' + error.message);
    }
};

function setupModalCloseButton() {
    const closeButton = document.querySelector('.speech-close');
    if (closeButton) {
        closeButton.addEventListener('click', function() {
            document.getElementById('speechRecognitionModal').style.display = 'none';
            stopRecording();
        });
        console.log('模態框關閉按鈕已設置');
    }
}

function setupSpeechRecognitionButton() {
    const recordButton = document.getElementById('recordButton');
    if (!recordButton) {
        console.error('找不到錄音按鈕');
        return;
    }
    
    console.log('設置錄音按鈕事件');
    
    // 移除可能存在的舊事件監聽器
    recordButton.removeEventListener('click', handleRecordButtonClick);
    recordButton.removeEventListener('mousedown', createRipple);
    recordButton.removeEventListener('touchstart', createRipple);
    
    // 添加新的事件監聽器
    recordButton.addEventListener('click', handleRecordButtonClick);
    
    // 對於移動設備，添加觸摸事件以提高響應速度
    recordButton.addEventListener('touchstart', handleButtonTouchStart, { passive: false });
    
    // 添加波紋效果
    recordButton.addEventListener('mousedown', createRipple);
    recordButton.addEventListener('touchstart', createRipple, { passive: true });
    
    // 改進按鈕樣式以增加可點擊性
    improveButtonStyles();
    
    console.log('錄音按鈕事件已設置');
}

// 改進按鈕樣式
function improveButtonStyles() {
    const recordButton = document.getElementById('recordButton');
    if (recordButton) {
        // 增加按鈕的可點擊區域和視覺反饋
        recordButton.style.cursor = 'pointer';
        recordButton.style.userSelect = 'none';
        recordButton.style.webkitTapHighlightColor = 'rgba(0,0,0,0)';
        
        // 添加:active樣式以提供直觀的視覺反饋
        const style = document.createElement('style');
        style.innerHTML = `
            #recordButton:active {
                transform: scale(0.98);
                background-color: #4338ca !important;
            }
            #recordButton.recording {
                background-color: #ef4444 !important;
                animation: pulse 2s infinite;
            }
            @keyframes pulse {
                0% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.4); }
                70% { box-shadow: 0 0 0 10px rgba(239, 68, 68, 0); }
                100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
            }
        `;
        document.head.appendChild(style);
    }
}

// 單獨的點擊處理函數
function handleRecordButtonClick(e) {
    e.preventDefault();
    e.stopPropagation();
    
    console.log('錄音按鈕被點擊');
    toggleRecording(this);
}

// 處理按鈕觸摸開始事件
function handleButtonTouchStart(e) {
    // 阻止默認行為以避免延遲
    e.preventDefault();
    e.stopPropagation();
    
    // 立即處理
    console.log('錄音按鈕被觸摸');
    toggleRecording(this);
}

// 切換錄音狀態
function toggleRecording(button) {
    // 防止快速連續點擊
    if (window.isToggling) {
        console.log('正在處理中，忽略重複點擊');
        return;
    }
    
    window.isToggling = true;
    
    setTimeout(() => {
        window.isToggling = false;
    }, 300); // 300ms防抖處理
    
    if (!window.isRecordingActive) {
        console.log('開始錄音...');
        window.isRecordingActive = true;
        button.classList.add('recording');
        const textEl = button.querySelector('.record-text');
        if (textEl) textEl.textContent = '點擊停止錄音';
        startRecording();
    } else {
        console.log('停止錄音...');
        window.isRecordingActive = false;
        button.classList.remove('recording');
        const textEl = button.querySelector('.record-text');
        if (textEl) textEl.textContent = '點擊開始錄音';
        stopRecording();
    }
}

function startRecording() {
    console.log('嘗試開始錄音...');
    
    if (!window.recognition) {
        console.error('語音辨識未初始化');
        alert('語音辨識未初始化，請重新載入頁面');
        window.isRecordingActive = false;
        window.isToggling = false;
        return;
    }
    
    // 立即設置錄音狀態和視覺反饋
    window.isRecording = true;
    
    // 立即創建和啟動波形動畫，不等待語音辨識啟動
    createWaveform();
    startWaveformAnimation();
    
    // 啟動語音辨識
    try {
        // 重要：設置onresult等事件處理器
        window.recognition.onresult = handleSpeechResult;
        window.recognition.onerror = handleSpeechError;
        window.recognition.onend = handleSpeechEnd;
        
        window.recognition.start();
        console.log('語音辨識已啟動');
    } catch (error) {
        console.error('無法啟動語音辨識:', error);
        
        // 如果發生錯誤，重置狀態
        window.isRecording = false;
        window.isRecordingActive = false;
        window.isToggling = false;
        
        const speechBtn = document.getElementById('recordButton');
        if (speechBtn) {
            speechBtn.classList.remove('recording');
            const textEl = speechBtn.querySelector('.record-text');
            if (textEl) textEl.textContent = '點擊開始錄音';
        }
        
        stopWaveformAnimation();
        
        // 顯示更友好的錯誤信息
        if (error.name === 'NotAllowedError') {
            alert('請允許使用麥克風以便使用語音辨識功能');
        } else {
            alert('語音辨識啟動失敗: ' + (error.message || '未知錯誤'));
        }
    }
}

function stopRecording() {
    console.log('嘗試停止錄音...');
    if (!window.isRecording) {
        console.log('錄音未開始，無需停止');
        return;
    }
    
    try {
        window.recognition.stop();
        console.log('語音辨識已停止');
    } catch (error) {
        console.error('無法停止語音辨識:', error);
        // 如果無法正常停止，手動觸發end事件
        handleSpeechEnd();
    }
}

function createWaveform() {
    console.log('創建波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (!waveformElement) {
        console.error('找不到波形容器');
        return;
    }
    
    waveformElement.innerHTML = '';
    window.waveformBars = [];
    
    const barCount = 30;
    
    for (let i = 0; i < barCount; i++) {
        const bar = document.createElement('div');
        bar.className = 'wave-bar';
        bar.style.height = '5px'; // 初始高度
        waveformElement.appendChild(bar);
        window.waveformBars.push(bar);
    }
    
    console.log(`已創建 ${barCount} 個波形條`);
}

function startWaveformAnimation() {
    console.log('開始波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (!waveformElement) {
        console.error('找不到波形容器');
        return;
    }
    
    waveformElement.classList.add('active');
    
    function updateWaveform() {
        if (!window.isRecording) {
            console.log('錄音已停止，不再更新波形');
            return;
        }
        
        // 模擬麥克風輸入
        if (window.waveformBars && window.waveformBars.length > 0) {
            for (let i = 0; i < window.waveformBars.length; i++) {
                const height = Math.floor(Math.random() * 25) + 5;
                window.waveformBars[i].style.height = `${height}px`;
            }
        }
        
        window.animationFrameId = requestAnimationFrame(updateWaveform);
    }
    
    updateWaveform();
    console.log('波形動畫已啟動');
}

function stopWaveformAnimation() {
    console.log('停止波形動畫');
    const waveformElement = document.querySelector('.waveform');
    if (waveformElement) {
        waveformElement.classList.remove('active');
    }
    
    if (window.animationFrameId) {
        cancelAnimationFrame(window.animationFrameId);
        window.animationFrameId = null;
    }
    
    // 重置所有波形條
    if (window.waveformBars) {
        window.waveformBars.forEach(bar => {
            if (bar) bar.style.height = '5px';
        });
    }
}

function handleSpeechResult(event) {
    console.log('接收到語音辨識結果', event);
    window.isRecording = false;
    stopWaveformAnimation();
    
    const speechBtn = document.getElementById('recordButton');
    if (speechBtn) {
        speechBtn.classList.remove('recording');
        const textEl = speechBtn.querySelector('.record-text');
        if (textEl) textEl.textContent = '點擊開始錄音';
    }
    
    // 確保結果有效
    if (!event || !event.results || !event.results[0] || !event.results[0][0]) {
        console.error('語音辨識結果無效');
        return;
    }
    
    const resultDisplay = document.querySelector('.recognition-result');
    const scoreDisplay = document.querySelector('.accuracy-score');
    
    if (!resultDisplay || !scoreDisplay) {
        console.error('找不到結果顯示元素');
        return;
    }
    
    const transcript = event.results[0][0].transcript.toLowerCase().trim();
    const confidence = event.results[0][0].confidence;
    
    console.log('辨識結果:', transcript, '置信度:', confidence);
    
    resultDisplay.textContent = `您說的是: "${transcript}"`;
    
    // 取得目標文字
    let targetText = '';
    if (currentCard === 1) {
        // 單字練習
        targetText = vocabularyData[currentCategory][currentWordIndex].word.toLowerCase();
    } else {
        // 例句練習
        if (vocabularyData[currentCategory][currentWordIndex].examples) {
            const exampleIndex = currentCard === 2 ? 0 : 1;
            if (vocabularyData[currentCategory][currentWordIndex].examples.length > exampleIndex) {
                targetText = vocabularyData[currentCategory][currentWordIndex].examples[exampleIndex].sentence.toLowerCase();
            }
        } else if (currentCard === 2 && vocabularyData[currentCategory][currentWordIndex].example) {
            targetText = vocabularyData[currentCategory][currentWordIndex].example.toLowerCase();
        }
    }
    
    console.log('目標文字:', targetText);
    
    // 文字相似度計算
    const similarity = calculateSimilarity(targetText, transcript);
    const percentScore = Math.round(similarity * 100);
    
    console.log('相似度:', similarity, '百分比分數:', percentScore);
    
    // 設置顏色等級
    let scoreClass = 'low';
    if (percentScore >= 80) {
        scoreClass = 'high';
    } else if (percentScore >= 60) {
        scoreClass = 'medium';
    }
    
    scoreDisplay.textContent = `準確度: ${percentScore}%`;
    scoreDisplay.className = 'accuracy-score ' + scoreClass;
    
    // 如果是單字練習，添加音節反饋
    if (currentCard === 1 && vocabularyData[currentCategory][currentWordIndex].syllables) {
        const syllablesContainer = document.createElement('div');
        syllablesContainer.className = 'syllable-feedback';
        
        const syllables = vocabularyData[currentCategory][currentWordIndex].syllables;
        const wordParts = splitTranscriptBySyllables(transcript, syllables);
        
        syllables.forEach((syllable, index) => {
            const syllableSpan = document.createElement('span');
            syllableSpan.className = 'syllable-item';
            syllableSpan.textContent = syllable;
            
            if (wordParts[index] && wordParts[index].match) {
                syllableSpan.classList.add('correct');
            } else {
                syllableSpan.classList.add('incorrect');
            }
            
            syllablesContainer.appendChild(syllableSpan);
        });
        
        // 清除先前的音節反饋
        const oldSyllableFeedback = document.querySelector('.syllable-feedback');
        if (oldSyllableFeedback) {
            oldSyllableFeedback.remove();
        }
        
        const feedbackElement = document.querySelector('.speech-feedback');
        if (feedbackElement) {
            feedbackElement.appendChild(syllablesContainer);
        }
    }
    
    // 重設錄音狀態
    window.isRecordingActive = false;
    window.isToggling = false;
}

function handleSpeechError(event) {
    console.error('語音辨識錯誤:', event.error);
    window.isRecording = false;
    stopWaveformAnimation();
    
    const speechBtn = document.getElementById('recordButton');
    if (speechBtn) {
        speechBtn.classList.remove('recording');
        const textEl = speechBtn.querySelector('.record-text');
        if (textEl) textEl.textContent = '點擊開始錄音';
    }
    
    const resultDisplay = document.querySelector('.recognition-result');
    if (resultDisplay) {
        resultDisplay.textContent = '無法辨識您的語音，請再試一次';
    }
    
    // 根據錯誤類型顯示適當的錯誤信息
    if (event.error === 'no-speech') {
        const scoreDisplay = document.querySelector('.accuracy-score');
        if (scoreDisplay) {
            scoreDisplay.textContent = '未檢測到語音，請嘗試說得更清晰或靠近麥克風';
            scoreDisplay.className = 'accuracy-score low';
        }
    }
    
    // 重設錄音狀態
    window.isRecordingActive = false;
    window.isToggling = false;
}

function handleSpeechEnd() {
    console.log('語音辨識結束');
    if (window.isRecording) {
        window.isRecording = false;
        stopWaveformAnimation();
        
        const speechBtn = document.getElementById('recordButton');
        if (speechBtn) {
            speechBtn.classList.remove('recording');
            const textEl = speechBtn.querySelector('.record-text');
            if (textEl) textEl.textContent = '點擊開始錄音';
        }
        
        // 重設錄音狀態
        window.isRecordingActive = false;
        window.isToggling = false;
    }
}

function showSpeechRecognitionModal() {
    console.log('顯示語音辨識模態框');
    const modal = document.getElementById('speechRecognitionModal');
    if (!modal) {
        console.error('找不到語音辨識模態框');
        return;
    }
    
    const targetDisplay = modal.querySelector('.target-word');
    if (!targetDisplay) {
        console.error('找不到目標文字顯示元素');
        return;
    }
    
    // 清除先前的結果
    const resultDisplay = modal.querySelector('.recognition-result');
    const scoreDisplay = modal.querySelector('.accuracy-score');
    const oldSyllableFeedback = modal.querySelector('.syllable-feedback');
    
    if (resultDisplay) resultDisplay.textContent = '';
    if (scoreDisplay) {
        scoreDisplay.textContent = '';
        scoreDisplay.className = 'accuracy-score';
    }
    
    if (oldSyllableFeedback) {
        oldSyllableFeedback.remove();
    }
    
    // 設置目標文字
    let targetText = '';
    if (currentCard === 1) {
        // 單字練習
        targetText = vocabularyData[currentCategory][currentWordIndex].word;
    } else {
        // 例句練習
        if (vocabularyData[currentCategory][currentWordIndex].examples) {
            const exampleIndex = currentCard === 2 ? 0 : 1;
            if (vocabularyData[currentCategory][currentWordIndex].examples.length > exampleIndex) {
                targetText = vocabularyData[currentCategory][currentWordIndex].examples[exampleIndex].sentence;
            }
        } else if (currentCard === 2 && vocabularyData[currentCategory][currentWordIndex].example) {
            targetText = vocabularyData[currentCategory][currentWordIndex].example;
        }
    }
    
    targetDisplay.textContent = targetText;
    console.log('設置目標文字:', targetText);
    
    // 創建波形
    createWaveform();
    
    // 設置關閉按鈕
    const closeButton = modal.querySelector('.speech-close');
    if (closeButton) {
        closeButton.onclick = function() {
            modal.style.display = 'none';
            stopRecording();
            window.isRecordingActive = false;
            window.isToggling = false;
            const recordButton = document.getElementById('recordButton');
            if (recordButton) {
                recordButton.classList.remove('recording');
                const textEl = recordButton.querySelector('.record-text');
                if (textEl) textEl.textContent = '點擊開始錄音';
            }
        };
    }
    
    // 顯示模態框
    modal.style.display = 'block';
    
    // 重置錄音狀態
    window.isRecordingActive = false;
    window.isToggling = false;
}

// 初始化語音辨識
function initializeSpeechRecognition() {
    try {
        window.recognition = new SpeechRecognition();
        window.recognition.lang = 'en-US';
        window.recognition.interimResults = false;
        window.recognition.maxAlternatives = 1;
        window.recognition.continuous = false;
        
        // 設置辨識結果處理函數
        window.recognition.onresult = handleSpeechResult;
        window.recognition.onerror = handleSpeechError;
        window.recognition.onend = handleSpeechEnd;
        
        // 初始化音頻分析器 (用於波形顯示)
        try {
            window.audioContext = new (window.AudioContext || window.webkitAudioContext)();
            window.analyser = window.audioContext.createAnalyser();
            window.analyser.fftSize = 256;
            console.log('音頻分析器初始化成功');
        } catch (error) {
            console.error('無法初始化音頻分析器', error);
        }
        
        console.log('語音辨識引擎已成功初始化');
        return true;
    } catch (error) {
        console.error('初始化語音辨識時發生錯誤:', error);
        return false;
    }
}
</script>
</body>
</html>
