## API Report File for "@angular/material_radio"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts

import { AfterContentInit } from '@angular/core';
import { AfterViewInit } from '@angular/core';
import { ControlValueAccessor } from '@angular/forms';
import { DoCheck } from '@angular/core';
import { ElementRef } from '@angular/core';
import { EventEmitter } from '@angular/core';
import { FocusOrigin } from '@angular/cdk/a11y';
import * as i0 from '@angular/core';
import * as i1 from '@angular/cdk/bidi';
import { InjectionToken } from '@angular/core';
import { OnDestroy } from '@angular/core';
import { OnInit } from '@angular/core';
import { QueryList } from '@angular/core';

// @public (undocumented)
export const MAT_RADIO_DEFAULT_OPTIONS: InjectionToken<MatRadioDefaultOptions>;

// @public @deprecated
export function MAT_RADIO_DEFAULT_OPTIONS_FACTORY(): MatRadioDefaultOptions;

// @public
export const MAT_RADIO_GROUP: InjectionToken<MatRadioGroup>;

// @public
export const MAT_RADIO_GROUP_CONTROL_VALUE_ACCESSOR: any;

// @public (undocumented)
export class MatRadioButton implements OnInit, AfterViewInit, DoCheck, OnDestroy {
    constructor(...args: unknown[]);
    ariaDescribedby: string;
    ariaLabel: string;
    ariaLabelledby: string;
    readonly change: EventEmitter<MatRadioChange>;
    get checked(): boolean;
    set checked(value: boolean);
    get color(): ThemePalette;
    set color(newValue: ThemePalette);
    get disabled(): boolean;
    set disabled(value: boolean);
    get disabledInteractive(): boolean;
    set disabledInteractive(value: boolean);
    disableRipple: boolean;
    // (undocumented)
    protected _elementRef: ElementRef<any>;
    focus(options?: FocusOptions, origin?: FocusOrigin): void;
    id: string;
    _inputElement: ElementRef<HTMLInputElement>;
    get inputId(): string;
    // (undocumented)
    _isRippleDisabled(): boolean;
    get labelPosition(): 'before' | 'after';
    set labelPosition(value: "before" | "after");
    _markForCheck(): void;
    name: string;
    // (undocumented)
    static ngAcceptInputType_checked: unknown;
    // (undocumented)
    static ngAcceptInputType_disabled: unknown;
    // (undocumented)
    static ngAcceptInputType_disabledInteractive: unknown;
    // (undocumented)
    static ngAcceptInputType_disableRipple: unknown;
    // (undocumented)
    static ngAcceptInputType_required: unknown;
    // (undocumented)
    static ngAcceptInputType_tabIndex: unknown;
    // (undocumented)
    ngAfterViewInit(): void;
    // (undocumented)
    ngDoCheck(): void;
    // (undocumented)
    ngOnDestroy(): void;
    // (undocumented)
    ngOnInit(): void;
    _noopAnimations: boolean;
    _onInputInteraction(event: Event): void;
    _onTouchTargetClick(event: Event): void;
    radioGroup: MatRadioGroup;
    get required(): boolean;
    set required(value: boolean);
    _rippleTrigger: ElementRef<HTMLElement>;
    protected _setDisabled(value: boolean): void;
    tabIndex: number;
    get value(): any;
    set value(value: any);
    // (undocumented)
    static ɵcmp: i0.ɵɵComponentDeclaration<MatRadioButton, "mat-radio-button", ["matRadioButton"], { "id": { "alias": "id"; "required": false; }; "name": { "alias": "name"; "required": false; }; "ariaLabel": { "alias": "aria-label"; "required": false; }; "ariaLabelledby": { "alias": "aria-labelledby"; "required": false; }; "ariaDescribedby": { "alias": "aria-describedby"; "required": false; }; "disableRipple": { "alias": "disableRipple"; "required": false; }; "tabIndex": { "alias": "tabIndex"; "required": false; }; "checked": { "alias": "checked"; "required": false; }; "value": { "alias": "value"; "required": false; }; "labelPosition": { "alias": "labelPosition"; "required": false; }; "disabled": { "alias": "disabled"; "required": false; }; "required": { "alias": "required"; "required": false; }; "color": { "alias": "color"; "required": false; }; "disabledInteractive": { "alias": "disabledInteractive"; "required": false; }; }, { "change": "change"; }, never, ["*"], true, never>;
    // (undocumented)
    static ɵfac: i0.ɵɵFactoryDeclaration<MatRadioButton, never>;
}

// @public
export class MatRadioChange<T = any> {
    constructor(
    source: MatRadioButton,
    value: T);
    source: MatRadioButton;
    value: T;
}

// @public (undocumented)
export interface MatRadioDefaultOptions {
    color: ThemePalette;
    disabledInteractive?: boolean;
}

// @public
export class MatRadioGroup implements AfterContentInit, OnDestroy, ControlValueAccessor {
    constructor(...args: unknown[]);
    readonly change: EventEmitter<MatRadioChange>;
    // (undocumented)
    _checkSelectedRadioButton(): void;
    color: ThemePalette;
    _controlValueAccessorChangeFn: (value: any) => void;
    get disabled(): boolean;
    set disabled(value: boolean);
    get disabledInteractive(): boolean;
    set disabledInteractive(value: boolean);
    _emitChangeEvent(): void;
    get labelPosition(): 'before' | 'after';
    set labelPosition(v: "before" | "after");
    // (undocumented)
    _markRadiosForCheck(): void;
    get name(): string;
    set name(value: string);
    // (undocumented)
    static ngAcceptInputType_disabled: unknown;
    // (undocumented)
    static ngAcceptInputType_disabledInteractive: unknown;
    // (undocumented)
    static ngAcceptInputType_required: unknown;
    ngAfterContentInit(): void;
    // (undocumented)
    ngOnDestroy(): void;
    onTouched: () => any;
    _radios: QueryList<MatRadioButton>;
    registerOnChange(fn: (value: any) => void): void;
    registerOnTouched(fn: any): void;
    get required(): boolean;
    set required(value: boolean);
    get selected(): MatRadioButton | null;
    set selected(selected: MatRadioButton | null);
    setDisabledState(isDisabled: boolean): void;
    _touch(): void;
    get value(): any;
    set value(newValue: any);
    writeValue(value: any): void;
    // (undocumented)
    static ɵdir: i0.ɵɵDirectiveDeclaration<MatRadioGroup, "mat-radio-group", ["matRadioGroup"], { "color": { "alias": "color"; "required": false; }; "name": { "alias": "name"; "required": false; }; "labelPosition": { "alias": "labelPosition"; "required": false; }; "value": { "alias": "value"; "required": false; }; "selected": { "alias": "selected"; "required": false; }; "disabled": { "alias": "disabled"; "required": false; }; "required": { "alias": "required"; "required": false; }; "disabledInteractive": { "alias": "disabledInteractive"; "required": false; }; }, { "change": "change"; }, ["_radios"], never, true, never>;
    // (undocumented)
    static ɵfac: i0.ɵɵFactoryDeclaration<MatRadioGroup, never>;
}

// @public (undocumented)
export class MatRadioModule {
    // (undocumented)
    static ɵfac: i0.ɵɵFactoryDeclaration<MatRadioModule, never>;
    // (undocumented)
    static ɵinj: i0.ɵɵInjectorDeclaration<MatRadioModule>;
    // (undocumented)
    static ɵmod: i0.ɵɵNgModuleDeclaration<MatRadioModule, never, [typeof MatCommonModule, typeof MatRippleModule, typeof MatRadioGroup, typeof MatRadioButton], [typeof MatCommonModule, typeof MatRadioGroup, typeof MatRadioButton]>;
}

// (No @packageDocumentation comment for this package)

```
