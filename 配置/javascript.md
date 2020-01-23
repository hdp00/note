```
//react antd
npm init
npm install react --save
npm install react-dom --save
npm install antd --save
npm install react-router-dom --save

//tds定义文件
//npm
npm install @types/react --save
npm install @types/react-dom --save
npm install @types/jquery --save
npm install @types/react-router-dom --save
//or typings
npm install typings -g
typings install dt~react
typings install dt~react-dom
typings install dt~jquery --global
typings install dt~require --global


//bug1
tsconfig.json中配置 "module": "amd",tsx文件中import { DatePicker } from 'antd'无法识别；必须改为"module": "commonjs"方可。

```

