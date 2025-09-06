<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <title>謎解きサイト</title>
    <style>
        body {
            font-family: sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #1f1e33; /* 背景色を変更 */
            color: white; /* 背景色に合わせて文字色を白に変更 */
        }
        #answer-box {
            padding: 10px;
            font-size: 16px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
        .correct {
            color: #00ff00; /* 正解時の文字色を明るい緑に変更 */
        }
        .incorrect {
            color: #ff0000; /* 不正解時の文字色を明るい赤に変更 */
        }
        #image-container img {
            max-width: 100%;
            height: auto;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>謎を解け！</h1>
    <p>ヒント：特定の文字列を入力してみよう</p>
    <input type="text" id="answer-box" placeholder="ここに入力">
    <button id="submit-button" onclick="checkAnswer()">送信</button>
    <p id="result-message"></p>
    <div id="image-container"></div>

    <script>
        // 間違えた回数をカウントする変数
        let incorrectCount = 0;
        // 正解の文字列
        const correctAnswer = '正解の文字列'; 
        const maxAttempts = 3;

        function checkAnswer() {
            const inputAnswer = document.getElementById('answer-box').value;
            const resultMessage = document.getElementById('result-message');
            const submitButton = document.getElementById('submit-button');
            const answerBox = document.getElementById('answer-box');
            const imageContainer = document.getElementById('image-container');

            if (inputAnswer === correctAnswer) {
                // 正解時の処理
                resultMessage.textContent = '正解！おめでとう！🎉';
                resultMessage.className = 'correct';

                // 画像を表示するための<img>要素を作成
                const correctImage = document.createElement('img');
                correctImage.src = 'きにゃこもち.jpg'; 
                correctImage.alt = '正解の画像';
                imageContainer.innerHTML = '';
                imageContainer.appendChild(correctImage);

                // 入力欄とボタンを無効化
                answerBox.disabled = true;
                submitButton.disabled = true;
            } else {
                // 不正解時の処理
                incorrectCount++;
                if (incorrectCount >= maxAttempts) {
                    // 3回間違えたら無効化
                    resultMessage.textContent = `残念、3回間違えました。これ以上入力できません。`;
                    resultMessage.className = 'incorrect';
                    answerBox.disabled = true;
                    submitButton.disabled = true;
                } else {
                    // 残り回数を表示
                    const remainingAttempts = maxAttempts - incorrectCount;
                    resultMessage.textContent = `不正解です。残り${remainingAttempts}回挑戦できます。`;
                    resultMessage.className = 'incorrect';
                }
            }
        }
    </script>
</body>
</html>
