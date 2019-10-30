# Electron-thermal-print
Electron printer plugin, currently supports 58mm, 
requires electron >= 4.x.x.  Inspired by 
[electron-thermal-printer](https://https://www.npmjs.com/package/electron-thermal-printer)

### Installation
```bash
$ npm install electron-thermal-print
```

### Usage
works in main and render processes
```js
const {PosPrinter} = require("electron-thermal-print");

const options = {
   preview: false,               // Preview in window or print
   width: '170px',               //  width of content body
   margin: '0 0 0 0',            // margin of content body
   copies: 1,                    // Number of copies to print
   printerName: 'XP-80C',        // printerName: string, check it at webContent.getPrinters()
   timeOutPerLine: 400
}

const data = [
   {
      type: 'text',                       // 'text' | 'barCode' | 'qrCode'
      value: 'SAMPLE HEADING',
      style: `text-align:center;`,
      css: {"font-weight": "700", "font-size": "18px"}
   }, {
      type: 'text',                       // 'text' | 'barCode' | 'qrCode'
      value: 'Secondary text',
      style: `text-align:left;color: red;`,
      css: {"text-decoration": "underline", "font-size": "10px"}
   },{
      type: 'barCode',
      value: 'HB4587896',
      height: 12,                     // height of barcode, applicable only to bar and QR codes
      width: 1,                       // width of barcode, applicable only to bar and QR codes
      displayValue: true,             // Display value below barcode
      fontsize: 8,
   },{
     type: 'qrCode',
      value: 'https://github.com/Hubertformin/electron-thermal-print',
      height: 55,
      width: 55,
      style: 'text-align:center;width:55px;margin: 10 20px 20 20px'
    }
]

PosPrinter.print(data, options)
 .then(() => {})
 .catch((error) => {
    console.error(error);
  });

```

## Typescript
### Usage

```typescript
import {PosPrinter, PosPrintData, PosPrintOptions} from "electron-thermal-print";

const options: PosPrintOptions = {
   preview: false,
   width: '170px',       
   margin: '0 0 0 0',    
   copies: 1,
   printerName: 'XP-80C',
   timeOutPerLine: 400
}

const data: PosPrintData = [
   {
      type: 'text',
      value: 'SAMPLE HEADING',
      style: `text-align:center;`,
      css: {"font-weight": "700", "font-size": "18px"}
   },{
      type: 'barCode',
      value: 'HB4587896',
      height: 12,
      width: 1,
      displayValue: true,
      fontsize: 8,
    },{
     type: 'qrCode',
      value: 'https://github.com/Hubertformin/electron-thermal-print',
      height: 55,
      width: 55,
      style: 'text-align:center;width:55px;margin: 10 20px 20 20px'
    }
]

PosPrinter.print(data, options)
 .then(() => {})
 .catch((error) => {
    console.error(error);
  });
```

## Printing options
| Options        |           |
| ------------- |:-------------|
| copies     | (number) number of copies to print |
| preview      | (boolean) preview in a window, default is false |
| width      | (string) width of a page       |
| margin | (string)  margin of a page, css values can be used   | 
| printerName | (string) the printer's name      | 
| timeOutPerLine | (number) timeout per line, default is 200      | 

## Print data object
Each object in `PosPrintData` array accounts for a row.

|           |                |
|-----------|:--------------|
| type      | (string) 'text', 'qrCode', 'barCode' |
| value | (string) value of the current row |
| height | (number) applicable to only bar and QR codes|
| width | (number)  applicable to only bar and QR codes|
| style | (string)  styles, css rules can be used |
| css | (string) css rules  ex: `{"font-size": "12px"}` |