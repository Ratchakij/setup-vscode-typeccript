# TypeScript Setup in VSCode (Run and Debug)
Setup a TypeScript project for development and debugging in VSCode 

# Step
1. npm init -y
2. npm i -g typescript
3. tsc --version
4. tsc --init --sourceMap --rootDir src --outDir dist
    \*
        --init: ใช้เพื่อสร้างไฟล์ tsconfig.json ใหม่ในโปรเจกต์
        --sourceMap: เปิดใช้งานการสร้างไฟล์ source map สำหรับการดีบัก
        --rootDir src: กำหนดไดเรกทอรีต้นทางที่ไฟล์ TypeScript ของคุณอยู่ (ในที่นี้คือ src)
        --outDir dist: กำหนดไดเรกทอรีปลายทางที่ไฟล์ JavaScript ที่คอมไพล์แล้วจะถูกเก็บไว้ (ในที่นี้คือ dist)
    \*
5. click Run and Debug -> create a launch.json file -> Node.js
6. create src/chicken.ts 
    \*
        // src/chicken.ts
        export class Chicken {
            voice() { console.log("cluck!!!"); }
        }
    \*
7. create src/index.ts
    \*
        // src/index.ts
        import { Chicken } from "./chicken";

        console.log("Hello TS");

        const chicken = new Chicken();
        chicken.voice();
    \*
8. terminal -> tsc
9. config .vscode\launch.json for debug after run command tsc
    \*
        // .vscode\launch.json
        "configurations": [
            {
                "program": "${workspaceFolder}\\dist\\index.js",
            }
        ]
    \*
10. npm i --save-dev typescript
11. Ctrl+Shift+P -> Tasks: Configure Default Build Task -> tsc: watch - tsconfig.json
12. Ctrl+Shift+P -> Tasks: Run Build Task // ถ้า terminal ใช้ git bash จะ error ให้เปลี่ยนไปใช้ power shell
    \*
        เปลี่ยน Default Terminal (เฉพาะ VS Code Terminal) ให้ Terminal ใช้ cmd หรือ PowerShell
        - เปิด Terminal (Ctrl + ~)
        - กด ไอคอน dropdown (˅) มุมขวาบน
        - คลิก "Select Default Profile"
        - เลือก Command Prompt หรือ PowerShell
        - ปิดแล้วเปิด Terminal ใหม่
    \*

# /* Setup nodemon */
1. npm i --save-dev nodemon ts-node
2. create nodemon.json
    \*
        // nodemon.json
        {
          "watch": ["src"],   
          "ext": "ts",        
          "ignore": ["src/**/*.test.ts"],  
          "exec": "ts-node ./src/index.ts"
        }
    \*
3. config package.json
    \*
        "scripts": {
          "dev": "nodemon",
        },
    \*