---
title: Referencing the Handsontable instance
metaTitle: Referencing the Handsontable instance - Guide - Handsontable Documentation
permalink: /next/angular-hot-reference
canonicalUrl: /angular-hot-reference
---

# Referencing the Handsontable instance

## Overview
The following example is an implementation of `@handsontable/angular`, which shows you how to reference the Handsontable instance from the wrapper component.

## Example
::: example :angular --html 1 --js 2
```html
<app-root></app-root>
```
```js
// app.component.ts
import { Component } from '@angular/core';
import Handsontable from 'handsontable/base';
import { HotTableRegisterer } from '@handsontable/angular';
import { createSpreadsheetData } from './helpers';

@Component({
  selector: 'app-root',
  template: `
  <div>
    <hot-table [hotId]="id" [settings]="hotSettings"></hot-table>
  </div>
  <br>
  <button (click)="swapHotData()" class="controls">Load new data</button>
  `,
})
class AppComponent {
  private hotRegisterer = new HotTableRegisterer();
  id = 'hotInstance';
  hotSettings: Handsontable.GridSettings = {
    data: createSpreadsheetData(4, 4),
    colHeaders: true,
    height: 'auto',
    licenseKey: 'non-commercial-and-evaluation'
  };

  swapHotData() {
    this.hotRegisterer.getInstance(this.id).loadData([['new', 'data']]);
  }
}

// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HotTableModule } from '@handsontable/angular';
import { registerAllModules } from 'handsontable/registry';

// register Handsontable's modules
registerAllModules();

@NgModule({
  imports:      [ BrowserModule, HotTableModule.forRoot() ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
class AppModule { }

// bootstrap
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

platformBrowserDynamic().bootstrapModule(AppModule).catch(err => { console.error(err) });
```
:::
