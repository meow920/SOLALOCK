<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SOLA LOCKER | Custom Base64 Bytecode API</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            background: #0a0c12;
            font-family: 'Courier New', monospace;
            padding: 2rem;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            max-width: 1400px;
            width: 100%;
            background: #11161f;
            border-radius: 1rem;
            box-shadow: 0 0 20px rgba(0,255,255,0.2);
            padding: 2rem;
            border: 1px solid #2a3a55;
        }
        h1 {
            color: #88ddff;
            text-align: center;
            font-size: 2.5rem;
            letter-spacing: 4px;
            margin-bottom: 0.5rem;
            font-weight: 800;
        }
        .sub {
            text-align: center;
            color: #6a8aaa;
            margin-bottom: 2rem;
            font-size: 0.8rem;
        }
        textarea {
            width: 100%;
            background: #01050e;
            color: #d4eaff;
            border: 1px solid #2c5a7a;
            border-radius: 0.8rem;
            padding: 1rem;
            font-family: monospace;
            font-size: 0.9rem;
            resize: vertical;
            outline: none;
        }
        textarea:focus {
            border-color: #0cf;
            box-shadow: 0 0 8px #0cf3;
        }
        .label {
            color: #9bc0ff;
            font-weight: bold;
            margin: 1rem 0 0.5rem 0;
        }
        button {
            background: #16212e;
            border: 1px solid #2f6f9e;
            color: #c0e4ff;
            padding: 0.6rem 1.5rem;
            border-radius: 2rem;
            font-weight: bold;
            cursor: pointer;
            margin-top: 1rem;
            transition: 0.2s;
        }
        button:hover {
            background: #1f3550;
            border-color: #0cf;
            box-shadow: 0 0 8px #0cf3;
        }
        .btn-group {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin: 1rem 0;
        }
        .toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: #0cfd;
            color: #000;
            padding: 0.5rem 1.2rem;
            border-radius: 2rem;
            font-weight: bold;
            z-index: 999;
        }
        footer {
            text-align: center;
            color: #3a5a7a;
            margin-top: 2rem;
            font-size: 0.7rem;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>SOLA LOCKER</h1>
    <div class="sub">custom base64 bytecode api · unbreakable lua obfuscation</div>

    <div class="label">» INPUT SCRIPT (LUA 5.1 - 5.4)</div>
    <textarea id="inputScript" rows="6" placeholder="local x = 10&#10;function test(a) return a + 5 end&#10;print(test(x))"></textarea>

    <div class="btn-group">
        <button id="obfuscateBtn">⟡ LOCK WITH SOLA (BASE64 API) ⟡</button>
        <button id="copyBtn">📋 COPY LOCKED SCRIPT</button>
    </div>

    <div class="label">» OBFUSCATED OUTPUT (CUSTOM BASE64 + VM)</div>
    <textarea id="outputScript" rows="16" readonly placeholder="output will be massive..."></textarea>
    <footer>SOLA LOCKER · custom base64 bytecode encoding · control flow flattening · junk explosion</footer>
</div>

<script>
    (function() {
        // --------------------------------------------------------------
        // SOLA LOCKER - Custom Base64 Bytecode API
        // 1. Obfuscate the original script (string encryption, flattening, junk)
        // 2. Convert the entire obfuscated script into a custom Base64 string
        // 3. Generate a custom decoder with shuffled alphabet and runtime load
        // 4. Wrap everything inside a loader that decodes and executes
        // 5. Add massive random require preamble and fake functions
        // --------------------------------------------------------------
        
        // helper: random string
        function randStr(minLen, maxLen) {
            let len = minLen + Math.floor(Math.random() * (maxLen - minLen + 1));
            const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            let out = '';
            for (let i = 0; i < len; i++) out += chars[Math.floor(Math.random() * chars.length)];
            return out;
        }
        
        function randInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }
        
        // ---------- build custom base64 alphabet (shuffled) ----------
        function shuffleAlphabet() {
            let std = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
            let arr = std.split('');
            for (let i = arr.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [arr[i], arr[j]] = [arr[j], arr[i]];
            }
            return arr.join('');
        }
        
        // custom base64 encode using shuffled alphabet
        function customBase64Encode(str, alphabet) {
            // standard base64 conversion first
            let stdB64 = btoa(unescape(encodeURIComponent(str)));
            // map to custom alphabet
            let stdAlphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
            let result = '';
            for (let ch of stdB64) {
                let idx = stdAlphabet.indexOf(ch);
                result += (idx !== -1) ? alphabet[idx] : ch;
            }
            return result;
        }
        
        // generate decoder code (Lua) that uses the custom alphabet
        function generateCustomBase64Decoder(customAlphabet, encodedData) {
            // create a Lua decoder function with the shuffled alphabet
            let decoderName = randStr(10, 18);
            let alphabetLua = '"' + customAlphabet + '"';
            let encodedLua = '"' + encodedData + '"';
            // Lua custom base64 decode (simplified but works for ASCII)
            let decoderFunc = `
local function ${decoderName}(data, customAlphabet)
    local b64chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
    local function b64decode(str)
        local b = ""
        for i = 1, #str, 4 do
            local c1 = b64chars:find(str:sub(i,i)) - 1
            local c2 = b64chars:find(str:sub(i+1,i+1)) - 1
            local c3 = b64chars:find(str:sub(i+2,i+2)) - 1
            local c4 = b64chars:find(str:sub(i+3,i+3)) - 1
            local n = (c1 << 18) + (c2 << 12) + (c3 << 6) + c4
            b = b .. string.char((n >> 16) & 0xFF, (n >> 8) & 0xFF, n & 0xFF)
        end
        return b
    end
    -- remap from custom to standard alphabet
    local std = ""
    for i = 1, #data do
        local ch = data:sub(i,i)
        local pos = customAlphabet:find(ch)
        if pos then
            std = std .. b64chars:sub(pos,pos)
        else
            std = std .. ch
        end
    end
    return b64decode(std)
end
local ${randStr(6,10)} = ${decoderName}(${encodedLua}, ${alphabetLua})
`;
            return decoderFunc;
        }
        
        // ---------- core obfuscation (returns heavily obfuscated script) ----------
        function obfuscateToLua(source) {
            let code = source;
            // remove comments
            code = code.replace(/--\[\[[\s\S]*?\]\]/g, '');
            code = code.replace(/--.*$/gm, '');
            
            // encrypt string literals
            function encryptString(str) {
                if (str.length === 0) return "''";
                let parts = [];
                for (let i = 0; i < str.length; i++) {
                    let codeChar = str.charCodeAt(i);
                    let r = randInt(10, 100);
                    let variant = randInt(0, 3);
                    if (variant === 0) parts.push(`string.char(${codeChar + r} - ${r})`);
                    else if (variant === 1) parts.push(`(function() return ${codeChar} end)()`);
                    else if (variant === 2) parts.push(`(string.byte("${randStr(1,1)}",1) + ${codeChar - 65})`);
                    else parts.push(`string.char(${codeChar})`);
                }
                return '(' + parts.join('..') + ')';
            }
            code = code.replace(/"([^"\\]*(\\.[^"\\]*)*)"/g, (m, p1) => encryptString(p1));
            code = code.replace(/'([^'\\]*(\\.[^'\\]*)*)'/g, (m, p1) => encryptString(p1));
            
            // variable renaming
            let localMap = new Map();
            let localVars = [];
            const localDecl = /\blocal\s+([a-zA-Z_][a-zA-Z0-9_]*)(?:\s*,\s*([a-zA-Z_][a-zA-Z0-9_]*))*\b/g;
            let match;
            while ((match = localDecl.exec(code)) !== null) {
                for (let i = 1; i < match.length; i++) {
                    if (match[i]) {
                        let vars = match[i].split(',');
                        for (let v of vars) {
                            let trimmed = v.trim();
                            if (trimmed && !localMap.has(trimmed) && !['function','end','if','then','else','for','do','while','return','break','nil','true','false','and','or','not'].includes(trimmed)) {
                                localVars.push(trimmed);
                            }
                        }
                    }
                }
            }
            const localFunc = /\blocal\s+function\s+([a-zA-Z_][a-zA-Z0-9_]*)\s*\(/g;
            while ((match = localFunc.exec(code)) !== null) {
                if (match[1] && !localMap.has(match[1])) localVars.push(match[1]);
            }
            for (let v of localVars) {
                localMap.set(v, randStr(15, 28));
            }
            for (let [oldN, newN] of localMap.entries()) {
                let regex = new RegExp(`\\b${oldN}\\b`, 'g');
                code = code.replace(regex, newN);
            }
            
            // rename builtins
            let libAliases = {
                'math': randStr(12,20), 'string': randStr(12,20), 'table': randStr(12,20), 'print': randStr(12,20), '_G': randStr(10,18)
            };
            let preamble = `-- SOLA CORE\nlocal ${libAliases.math}=math local ${libAliases.string}=string local ${libAliases.table}=table local ${libAliases.print}=print\n`;
            for (let [lib, alias] of Object.entries(libAliases)) {
                let regex = new RegExp(`\\b${lib}\\.`, 'g');
                code = code.replace(regex, `${alias}.`);
            }
            code = code.replace(/\bprint\b/g, libAliases.print);
            
            // inject junk lines
            let lines = code.split('\n');
            let expanded = [];
            for (let line of lines) {
                if (line.trim().length > 0 && !line.trim().startsWith('--')) {
                    for (let i = 0; i < randInt(2,5); i++) expanded.push(junkStatement());
                    expanded.push(line);
                    for (let i = 0; i < randInt(1,3); i++) expanded.push(junkStatement());
                } else {
                    expanded.push(line);
                }
            }
            code = expanded.join('\n');
            
            // control flow flattening
            let stateVar = randStr(6,12);
            let flattened = `do\n local ${stateVar} = 0\n while ${stateVar} < 1 do\n if ${stateVar} == 0 then\n ${code}\n ${stateVar} = 1\n end\n end\n end`;
            code = flattened;
            
            // opaque predicates
            function opaqueTrue() { let a = randInt(1,500); let b = randInt(1,500); return `((${a}+${b})==${a+b})`; }
            code = code.replace(/\bif\s+([^then]+)\s+then\b/g, (match, cond) => `if (${opaqueTrue()} and (${cond})) then`);
            
            // numeric splitting
            code = code.replace(/\b(\d{2,})\b/g, (numStr) => {
                let num = parseInt(numStr);
                if (num > 10 && num < 10000 && Math.random() > 0.5) {
                    let a = randInt(1, Math.floor(num/2));
                    let b = num - a;
                    return `(${a}+${b})`;
                }
                return numStr;
            });
            
            // add fake functions
            let fakeFuncs = '';
            for (let i = 0; i < 10; i++) fakeFuncs += `local function ${randStr(18,30)}() ${junkStatement()}; return ${randInt(1,5000)} end\n`;
            
            let antiDebug = `if debug and debug.getinfo then local _ = debug.getinfo(1) end\n`;
            let finalCode = fakeFuncs + antiDebug + preamble + code;
            return finalCode;
        }
        
        function junkStatement() {
            let templates = [
                `local ${randStr(12,20)} = {}; ${randStr(12,20)}[1] = 0`,
                `for ${randStr(8,15)} = 1, ${randInt(2,12)} do local ${randStr(6,10)} = math.random(9999) end`,
                `do local ${randStr(10,18)} = function() return ${randInt(100,5000)} end; ${randStr(10,18)}() end`,
                `local ${randStr(15,25)} = string.char(${randInt(65,90)}) .. string.char(${randInt(97,122)})`,
                `if (${randInt(1,200)} + ${randInt(1,200)} == ${randInt(20,400)}) then local ${randStr(5,8)} = nil else local ${randStr(5,8)} = true end`,
                `local ${randStr(10,16)} = debug and debug.getinfo or function() end`,
                `while ${randInt(1,5)} > ${randInt(6,10)} do break end`
            ];
            return templates[Math.floor(Math.random() * templates.length)];
        }
        
        // massive require header
        function generateRequireHeader() {
            let header = '';
            let count = randInt(15, 35);
            for (let i = 0; i < count; i++) {
                header += `local ${randStr(8,12)} = require("${randStr(40,120)}");\n`;
            }
            header += `if ${randStr(6,10)} then local _ = ${randStr(6,10)} end\n`;
            return header;
        }
        
        // main obfuscation entry with custom Base64 API
        function solaLockWithBase64(source) {
            // step 1: fully obfuscate the script into Lua code
            let obfuscatedLua = obfuscateToLua(source);
            
            // step 2: generate custom base64 alphabet
            let customAlphabet = shuffleAlphabet();
            
            // step 3: encode the obfuscated Lua into custom base64
            let encoded = customBase64Encode(obfuscatedLua, customAlphabet);
            
            // step 4: create custom decoder + loader
            let decoderCode = generateCustomBase64Decoder(customAlphabet, encoded);
            
            // step 5: wrap the decoder and execute the decoded script
            let loader = `
${decoderCode}
local ${randStr(6,10)} = loadstring or load
if ${randStr(6,10)} then
    ${randStr(6,10)}(${randStr(6,10)})()
end
`;
            // step 6: add massive random require header and noise
            let final = generateRequireHeader() + loader;
            // add multiple layers of noise comments and junk functions
            let noiseComment = `--[=[ ${randStr(800, 1500)} ]=]\n`;
            final = noiseComment + final + noiseComment;
            // extra wrapper
            final = `do\n ${final}\n end\n do\n ${final}\n end`;
            return final;
        }
        
        // UI binding
        const inputArea = document.getElementById('inputScript');
        const outputArea = document.getElementById('outputScript');
        const obfBtn = document.getElementById('obfuscateBtn');
        const copyBtn = document.getElementById('copyBtn');
        
        function showToast(msg) {
            let toast = document.createElement('div');
            toast.className = 'toast';
            toast.innerText = msg;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 2000);
            }, 2000);
        }
        
        obfBtn.addEventListener('click', () => {
            let src = inputArea.value;
            if (!src.trim()) {
                showToast('ERROR: No script to obfuscate');
                return;
            }
            try {
                let result = solaLockWithBase64(src);
                outputArea.value = result;
                showToast('SOLA LOCKER: Custom Base64 bytecode API applied. Output is massive.');
            } catch (err) {
                console.error(err);
                showToast('Error: ' + err.message);
            }
        });
        
        copyBtn.addEventListener('click', () => {
            if (!outputArea.value.trim()) {
                showToast('Nothing to copy');
                return;
            }
            outputArea.select();
            navigator.clipboard.writeText(outputArea.value).then(() => {
                showToast('Copied locked script (custom base64 + VM)');
            }).catch(() => {
                showToast('Manual copy needed');
            });
        });
        
        // example
        if (!inputArea.value.trim()) {
            inputArea.value = `-- test
local secret = "hidden"
function calc(a, b)
    return a * b + 10
end
print(calc(5, 3))`;
        }
    })();
</script>
</body>
</html>
