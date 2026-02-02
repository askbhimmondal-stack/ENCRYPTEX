
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ENCRYPTEX</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Courier New', monospace;
        }
        
        body {
            background: #0a0a0a;
            color: #00ff00;
            min-height: 100vh;
            padding: 20px;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(0, 40, 0, 0.2) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(0, 40, 0, 0.2) 0%, transparent 20%);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            margin: 0 auto;
            border: 1px solid #003300;
            border-radius: 5px;
            padding: 20px;
            background: rgba(0, 20, 0, 0.7);
            box-shadow: 0 0 20px rgba(0, 255, 0, 0.1);
            position: relative;
            overflow: hidden;
        }
        
        .container::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: linear-gradient(90deg, transparent, #00ff00, transparent);
            animation: scanline 3s linear infinite;
        }
        
        @keyframes scanline {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px dashed #003300;
        }
        
        h1 {
            font-size: 28px;
            color: #00cc00;
            text-shadow: 0 0 5px #00ff00;
            letter-spacing: 2px;
        }
        
        .subtitle {
            font-size: 14px;
            color: #009900;
            margin-top: 5px;
        }
        
        .input-section, .output-section {
            margin-bottom: 25px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #00cc00;
        }
        
        textarea {
            width: 100%;
            height: 120px;
            background: rgba(0, 10, 0, 0.8);
            border: 1px solid #003300;
            border-radius: 3px;
            color: #00ff00;
            padding: 12px;
            font-size: 16px;
            resize: vertical;
        }
        
        textarea:focus {
            outline: none;
            border-color: #00cc00;
            box-shadow: 0 0 5px rgba(0, 255, 0, 0.3);
        }
        
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .control-group {
            flex: 1;
            min-width: 200px;
        }
        
        select, button, input {
            width: 100%;
            padding: 10px;
            background: rgba(0, 30, 0, 0.8);
            border: 1px solid #003300;
            border-radius: 3px;
            color: #00ff00;
            font-size: 14px;
        }
        
        select:focus, button:focus, input:focus {
            outline: none;
            border-color: #00cc00;
        }
        
        button {
            background: rgba(0, 50, 0, 0.8);
            cursor: pointer;
            transition: all 0.3s;
            font-weight: bold;
            letter-spacing: 1px;
        }
        
        button:hover {
            background: rgba(0, 70, 0, 0.9);
            box-shadow: 0 0 10px rgba(0, 255, 0, 0.3);
        }
        
        .output-section textarea {
            background: rgba(0, 15, 0, 0.9);
        }
        
        .status {
            text-align: center;
            margin-top: 10px;
            font-size: 14px;
            color: #009900;
            min-height: 20px;
        }
        
        .flashing {
            animation: flash 1s infinite;
        }
        
        @keyframes flash {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        footer {
            text-align: center;
            margin-top: 30px;
            font-size: 12px;
            color: #006600;
            border-top: 1px dashed #003300;
            padding-top: 15px;
        }
        
        .action-buttons {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        
        .action-buttons button {
            flex: 1;
        }
        
        @media (max-width: 600px) {
            .controls {
                flex-direction: column;
            }
            
            .control-group {
                min-width: 100%;
            }
            
            .action-buttons {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>ENCRYPTEX</h1>
            <div class="subtitle">Understand her Love Language </div>
        </header>
        
        <div class="input-section">
            <label for="inputText">MESSAGE:</label>
            <textarea id="inputText" placeholder="Enter message here..."></textarea>
        </div>
        
        <div class="controls">
            <div class="control-group">
                <label for="cipherMethod">CIPHER METHOD:</label>
                <select id="cipherMethod">
                    <option value="reverse">Reverse Text</option>
                    <option value="caesar">Caesar Cipher</option>
                    <option value="atbash">Atbash Cipher</option>
                    <option value="morse">Morse Code</option>
                    <option value="railfence">Rail Fence Cipher</option>
                    <option value="keyword">Keyword Cipher</option>
                    <option value="vigenere">Vigenère Cipher</option>
                    <option value="base64">Base64</option>
                </select>
            </div>
            
            <div class="control-group" id="keyContainer">
                <label for="cipherKey">KEY:</label>
                <input type="text" id="cipherKey" placeholder="Enter key if required">
            </div>
            
            <div class="control-group">
                <label>ACTION:</label>
                <div class="action-buttons">
                    <button id="encodeBtn">ENCODE</button>
                    <button id="decodeBtn">DECODE</button>
                </div>
            </div>
        </div>
        
        <div class="output-section">
            <label for="outputText">RESULT:</label>
            <textarea id="outputText" readonly></textarea>
        </div>
        
        <div class="status" id="statusMessage">READY FOR OPERATION</div>
        
        <footer>
            <div>CONFIDENTIAL - UNAUTHORIZED ACCESS PROHIBITED</div>
            <div>VERSION 7.3.2 - ENCRYPTION LEVEL: MAXIMUM</div>
            <div>Made in ❤️ for Pooja</div>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const inputText = document.getElementById('inputText');
            const outputText = document.getElementById('outputText');
            const cipherMethod = document.getElementById('cipherMethod');
            const cipherKey = document.getElementById('cipherKey');
            const decodeBtn = document.getElementById('decodeBtn');
            const encodeBtn = document.getElementById('encodeBtn');
            const statusMessage = document.getElementById('statusMessage');
            const keyContainer = document.getElementById('keyContainer');
            
            // Update key field visibility based on selected method
            cipherMethod.addEventListener('change', function() {
                const method = this.value;
                if (method === 'caesar' || method === 'railfence' || method === 'keyword' || method === 'vigenere') {
                    keyContainer.style.display = 'block';
                    
                    if (method === 'caesar') {
                        cipherKey.placeholder = 'Shift amount (e.g., 3)';
                    } else if (method === 'railfence') {
                        cipherKey.placeholder = 'Number of rails (e.g., 3)';
                    } else if (method === 'keyword' || method === 'vigenere') {
                        cipherKey.placeholder = 'Keyword (e.g., SECRET)';
                    }
                } else {
                    keyContainer.style.display = 'none';
                }
            });
            
            // Initial setup
            keyContainer.style.display = 'none';
            
            // Decode button click handler
            decodeBtn.addEventListener('click', function() {
                processText('decode');
            });
            
            // Encode button click handler
            encodeBtn.addEventListener('click', function() {
                processText('encode');
            });
            
            function processText(action) {
                const text = inputText.value.trim();
                const method = cipherMethod.value;
                const key = cipherKey.value.trim();
                
                if (!text) {
                    setStatus('ERROR: NO INPUT TEXT PROVIDED', true);
                    return;
                }
                
                setStatus(`${action.toUpperCase()}ING IN PROGRESS...`, true);
                
                // Simulate processing with a slight delay
                setTimeout(() => {
                    try {
                        const result = processWithMethod(text, method, key, action);
                        outputText.value = result;
                        setStatus(`MESSAGE SUCCESSFULLY ${action.toUpperCase()}D`, false);
                    } catch (error) {
                        outputText.value = '';
                        setStatus(`${action.toUpperCase()}ING FAILED: ` + error.message, true);
                    }
                }, 800);
            }
            
            function setStatus(message, isError) {
                statusMessage.textContent = message;
                statusMessage.className = 'status ' + (isError ? 'flashing' : '');
                statusMessage.style.color = isError ? '#ff3300' : '#00cc00';
            }
            
            function processWithMethod(text, method, key, action) {
                switch(method) {
                    case 'reverse':
                        return action === 'encode' ? encodeReverse(text) : decodeReverse(text);
                    case 'caesar':
                        return action === 'encode' ? encodeCaesar(text, parseInt(key) || 3) : decodeCaesar(text, parseInt(key) || 3);
                    case 'atbash':
                        // Atbash is its own inverse
                        return decodeAtbash(text);
                    case 'morse':
                        return action === 'encode' ? encodeMorse(text) : decodeMorse(text);
                    case 'railfence':
                        return action === 'encode' ? encodeRailFence(text, parseInt(key) || 3) : decodeRailFence(text, parseInt(key) || 3);
                    case 'keyword':
                        return action === 'encode' ? encodeKeyword(text, key || 'SECRET') : decodeKeyword(text, key || 'SECRET');
                    case 'vigenere':
                        return action === 'encode' ? encodeVigenere(text, key || 'KEY') : decodeVigenere(text, key || 'KEY');
                    case 'base64':
                        return action === 'encode' ? encodeBase64(text) : decodeBase64(text);
                    default:
                        throw new Error('Unknown cipher method');
                }
            }
            
            function decodeReverse(text) {
                return text.split('').reverse().join('');
            }
            
            function encodeReverse(text) {
                return decodeReverse(text); // Same operation for encode/decode
            }
            
            function decodeCaesar(text, shift) {
                shift = (26 - shift) % 26; // For decoding, we reverse the shift
                return text.replace(/[a-z]/gi, function(char) {
                    const base = char < 'a' ? 65 : 97;
                    return String.fromCharCode(((char.charCodeAt(0) - base + shift) % 26) + base);
                });
            }
            
            function encodeCaesar(text, shift) {
                return text.replace(/[a-z]/gi, function(char) {
                    const base = char < 'a' ? 65 : 97;
                    return String.fromCharCode(((char.charCodeAt(0) - base + shift) % 26) + base);
                });
            }
            
            function decodeAtbash(text) {
                return text.replace(/[a-z]/gi, function(char) {
                    const base = char < 'a' ? 65 : 97;
                    return String.fromCharCode(25 - (char.charCodeAt(0) - base) + base);
                });
            }
            
            function decodeMorse(text) {
                const morseMap = {
                    '.-': 'A', '-...': 'B', '-.-.': 'C', '-..': 'D', '.': 'E',
                    '..-.': 'F', '--.': 'G', '....': 'H', '..': 'I', '.---': 'J',
                    '-.-': 'K', '.-..': 'L', '--': 'M', '-.': 'N', '---': 'O',
                    '.--.': 'P', '--.-': 'Q', '.-.': 'R', '...': 'S', '-': 'T',
                    '..-': 'U', '...-': 'V', '.--': 'W', '-..-': 'X', '-.--': 'Y',
                    '--..': 'Z', '.----': '1', '..---': '2', '...--': '3', '....-': '4',
                    '.....': '5', '-....': '6', '--...': '7', '---..': '8', '----.': '9',
                    '-----': '0', '--..--': ',', '.-.-.-': '.', '..--..': '?', '-..-.': '/',
                    '-....-': '-', '-.--.': '(', '-.--.-': ')', '.-...': '&', '---...': ':',
                    '-.-.-.': ';', '-...-': '=', '.-.-.': '+', '.----.': "'", '..--.-': '_',
                    '.-..-.': '"', '...-..-': '$', '.--.-.': '@', '/': ' '
                };
                
                return text.split('/').map(word => 
                    word.split(' ').map(code => morseMap[code] || '?').join('')
                ).join(' ');
            }
            
            function encodeMorse(text) {
                const reverseMorseMap = {
                    'A': '.-', 'B': '-...', 'C': '-.-.', 'D': '-..', 'E': '.',
                    'F': '..-.', 'G': '--.', 'H': '....', 'I': '..', 'J': '.---',
                    'K': '-.-', 'L': '.-..', 'M': '--', 'N': '-.', 'O': '---',
                    'P': '.--.', 'Q': '--.-', 'R': '.-.', 'S': '...', 'T': '-',
                    'U': '..-', 'V': '...-', 'W': '.--', 'X': '-..-', 'Y': '-.--',
                    'Z': '--..', '1': '.----', '2': '..---', '3': '...--', '4': '....-',
                    '5': '.....', '6': '-....', '7': '--...', '8': '---..', '9': '----.',
                    '0': '-----', ',': '--..--', '.': '.-.-.-', '?': '..--..', '/': '-..-.',
                    '-': '-....-', '(': '-.--.', ')': '-.--.-', '&': '.-...', ':': '---...',
                    ';': '-.-.-.', '=': '-...-', '+': '.-.-.', "'": '.----.', '_': '..--.-',
                    '"': '.-..-.', '$': '...-..-', '@': '.--.-.', ' ': '/'
                };
                
                return text.toUpperCase().split('').map(char => 
                    reverseMorseMap[char] || '?'
                ).join(' ');
            }
            
            function decodeRailFence(text, rails) {
                if (rails < 2) return text;
                
                // Create the fence pattern
                const fence = [];
                for (let i = 0; i < rails; i++) fence.push([]);
                
                // Fill the fence with placeholder values
                let rail = 0;
                let direction = 1;
                const positions = Array(rails).fill(0);
                
                for (let i = 0; i < text.length; i++) {
                    fence[rail][positions[rail]] = i;
                    positions[rail]++;
                    
                    if (rail === 0) direction = 1;
                    else if (rail === rails - 1) direction = -1;
                    
                    rail += direction;
                }
                
                // Flatten the fence to get the reading order
                const order = [];
                for (let r = 0; r < rails; r++) {
                    for (let c = 0; c < fence[r].length; c++) {
                        order[fence[r][c]] = text[order.length];
                    }
                }
                
                // Read the fence in zigzag pattern to decode
                let result = '';
                rail = 0;
                direction = 1;
                const railChars = Array(rails).fill(0);
                
                for (let i = 0; i < text.length; i++) {
                    result += order[fence[rail][railChars[rail]]];
                    railChars[rail]++;
                    
                    if (rail === 0) direction = 1;
                    else if (rail === rails - 1) direction = -1;
                    
                    rail += direction;
                }
                
                return result;
            }
            
            function encodeRailFence(text, rails) {
                if (rails < 2) return text;
                
                const fence = [];
                for (let i = 0; i < rails; i++) fence.push([]);
                
                let rail = 0;
                let direction = 1;
                
                for (let i = 0; i < text.length; i++) {
                    fence[rail].push(text[i]);
                    
                    if (rail === 0) direction = 1;
                    else if (rail === rails - 1) direction = -1;
                    
                    rail += direction;
                }
                
                return fence.map(row => row.join('')).join('');
            }
            
            function decodeKeyword(text, keyword) {
                // Create substitution alphabet based on keyword
                const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
                let cipherAlphabet = '';
                
                // Add unique letters from keyword
                for (let char of keyword.toUpperCase()) {
                    if (!cipherAlphabet.includes(char) && alphabet.includes(char)) {
                        cipherAlphabet += char;
                    }
                }
                
                // Add remaining letters from alphabet
                for (let char of alphabet) {
                    if (!cipherAlphabet.includes(char)) {
                        cipherAlphabet += char;
                    }
                }
                
                // Create mapping from cipher to plain
                const mapping = {};
                for (let i = 0; i < alphabet.length; i++) {
                    mapping[cipherAlphabet[i]] = alphabet[i];
                }
                
                // Apply the mapping to decode
                return text.toUpperCase().replace(/[A-Z]/g, char => mapping[char] || char);
            }
            
            function encodeKeyword(text, keyword) {
                // Create substitution alphabet based on keyword
                const alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
                let cipherAlphabet = '';
                
                // Add unique letters from keyword
                for (let char of keyword.toUpperCase()) {
                    if (!cipherAlphabet.includes(char) && alphabet.includes(char)) {
                        cipherAlphabet += char;
                    }
                }
                
                // Add remaining letters from alphabet
                for (let char of alphabet) {
                    if (!cipherAlphabet.includes(char)) {
                        cipherAlphabet += char;
                    }
                }
                
                // Create mapping from plain to cipher
                const mapping = {};
                for (let i = 0; i < alphabet.length; i++) {
                    mapping[alphabet[i]] = cipherAlphabet[i];
                }
                
                // Apply the mapping to encode
                return text.toUpperCase().replace(/[A-Z]/g, char => mapping[char] || char);
            }
            
            function decodeVigenere(text, key) {
                key = key.toUpperCase().replace(/[^A-Z]/g, '');
                if (!key) return text;
                
                let result = '';
                let keyIndex = 0;
                
                for (let i = 0; i < text.length; i++) {
                    const char = text[i];
                    if (/[A-Z]/i.test(char)) {
                        const base = char < 'a' ? 65 : 97;
                        const keyChar = key[keyIndex % key.length];
                        const keyShift = keyChar.charCodeAt(0) - 65;
                        
                        // For decoding, we subtract the key shift
                        const decodedCharCode = ((char.toUpperCase().charCodeAt(0) - 65 - keyShift + 26) % 26) + base;
                        result += String.fromCharCode(decodedCharCode);
                        
                        keyIndex++;
                    } else {
                        result += char;
                    }
                }
                
                return result;
            }
            
            function encodeVigenere(text, key) {
                key = key.toUpperCase().replace(/[^A-Z]/g, '');
                if (!key) return text;
                
                let result = '';
                let keyIndex = 0;
                
                for (let i = 0; i < text.length; i++) {
                    const char = text[i];
                    if (/[A-Z]/i.test(char)) {
                        const base = char < 'a' ? 65 : 97;
                        const keyChar = key[keyIndex % key.length];
                        const keyShift = keyChar.charCodeAt(0) - 65;
                        
                        const encodedCharCode = ((char.toUpperCase().charCodeAt(0) - 65 + keyShift) % 26) + base;
                        result += String.fromCharCode(encodedCharCode);
                        
                        keyIndex++;
                    } else {
                        result += char;
                    }
                }
                
                return result;
            }
            
            function encodeBase64(text) {
                return btoa(text);
            }
            
            function decodeBase64(text) {
                try {
                    return atob(text);
                } catch (e) {
                    throw new Error('Invalid Base64 string');
                }
            }
        });
    </script>
</body>
</html>


# ENCRYPTEX
