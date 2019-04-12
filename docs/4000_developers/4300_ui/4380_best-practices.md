---
title: "Best Practices"
parent: Developers
grand_parent: UI
nav_order: 4380
permalink: /docs/developers/ui/best-practices.html
---

# Best Practices

## Ordered Formular

```html
  <form *ngIf="!loading" #createForm="ngForm">
    <ion-row>
      <ion-col col-12 col-md-3>
        <ion-item>
          ...
        </ion-item>
      </ion-col>
    </ion-row>
  </form>
```

## Check field is valid

```ts
  /**
   * Checks if a form property is touched and invalid.
   *
   * @param      {string}   paramName  name of the form property that should be checked
   * @return     {boolean}  true if touched and invalid, else false
   */
  showError(paramName: string) {
    if (this.createForm) {
      return this.createForm.controls[paramName].invalid &&
        this.createForm.controls[paramName].touched;
    }
  }  
```

## Normal Input
```html
  <ion-item>
    <ion-label stacked>{{ 'field.text' | translate }}*</ion-label>
    <ion-input name="field" required
      [(ngModel)]="formData.field"
      [placeholder]="'field.desc' | translate"
      (ionChange)="ref.detectChanges()">
    </ion-input>
  </ion-item>
  <ion-chip class="error-hint" *ngIf="showError('field')" color="danger">
    <ion-icon name="close" color="danger"></ion-icon>
    <ion-label>{{ 'field.error' | translate }}</ion-label>
  </ion-chip>
```

## Select Input

```html
    <ion-item>
      <ion-label stacked>{{ 'select.text' | translate }}*</ion-label>

      <ion-select name="select" interface="popover"
       [(ngModel)]="formData.select"
       [placeholder]="'select.desc' | translate"
       (ionChange)="ref.detectChanges()">
        <ion-option value="0">{{ 'select.value0' | translate }}</ion-option>      
        <ion-option value="1">{{ 'select.value1' | translate }}</ion-option>
      </ion-select>
    </ion-item>
    <ion-chip class="error-hint" *ngIf="showError('select')" color="danger">
      <ion-icon name="close" color="danger"></ion-icon>
      <ion-label>{{ 'select.error' | translate }}</ion-label>
    </ion-chip>
```

## DateTime Input

```html
  <ion-item>
    <ion-label stacked>{{ 'date.text' | translate }}*</ion-label>
    <ion-datetime name="startDate"
      required="true"
      displayFormat="DD-MM-YYYY H:mm"
      pickerFormat="DD-MMM-YYYY HH:mm"
      [(ngModel)]="formData.startDate"
      [placeholder]="'startDate.text' | translate"
      [cancelText]="'cancel' | translate"
      [doneText]="'done' | translate"
      minuteValues="0,15,30,45"
      [monthShortNames]="translateService.monthShortNames"
      (ionChange)="ref.detectChanges()">
    </ion-datetime>
  </ion-item>
  <ion-chip class="error-hint" *ngIf="showError('startDate')" color="danger">
    <ion-icon name="close" color="danger"></ion-icon>
    <ion-label>{{ 'startDate.error' | translate }}</ion-label>
  </ion-chip>
```

## Contract members Input

```html
  <ion-col>
    <contract-members #members
      [(members)]="formData.members"
      (onChange)="ref.detectChanges()">
      <h3 label>{{ 'custom-label' | translate }}</h3>
    </contract-members>
    <ion-chip class="error-hint"
      *ngIf="formData.members.length === 0 && members.touched"
      color="danger">
      <ion-icon name="close" color="danger"></ion-icon>
      <ion-label>{{ 'members.error' | translate }}</ion-label>
    </ion-chip>
  </ion-col>
```

### More Coming soon...