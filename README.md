# Practice  https://github.com/mathewhaug/My-First-Angular-App-f24/tree/Lecture-4



[11:44 a.m., 2024-12-13] Aarsh: Pipes

import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'goodKitty',
})
export class GoodKittyPipe implements PipeTransform {
  transform(isGoodKitty: boolean): string {
    return isGoodKitty
      ? 'This is a good kitty!'
      : 'All cats are good cats';
  }
}

@Pipe({
  name: 'defaultPicture',
})
export class DefaultPicturePipe implements PipeTransform {
  transform(pictureUrl: string): string {
    return pictureUrl || 'assets/DefaultPicture.png';
  }
}


Directives 


import { Directive, ElementRef, Input, Renderer2 } from '@angular/core';

@Directive({
  selector: '[highlightGoodKitty]',
})
export class HighlightGoodKittyDirective {
  @Input() set highlightGoodKitty(isGoodKitty: boolean) {
    if (isGoodKitty) {
      this.renderer.setStyle(
        this.el.nativeElement,
        'background-color',
        'yellow'
      );
    }
  }

  constructor(private el: ElementRef, private renderer: Renderer2) {}
}


import { Directive, Renderer2, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[flashBackground]',
})
export class FlashBackgroundDirective {
  private colors: string[] = ['red', 'yellow', 'blue'];
  private currentIndex = 0;

  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.flash();
  }

  private flash() {
    const color = this.colors[this.currentIndex];
    this.renderer.setStyle(this.el.nativeElement, 'background-color', color);
    this.currentIndex = (this.currentIndex + 1) % this.colors.length;
    setTimeout(() => this.flash(), 500); // Change every 500ms
  }
}


Reactive form 



import { Component } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';

@Component({
  selector: 'app-cat-form',
  templateUrl: './cat-form.component.html',
})
export class CatFormComponent {
  catForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.catForm = this.fb.group({
      name: [''],
      age: [''],
      picture: [''],
    });
  }

  onSubmit() {
    console.log(this.catForm.value);
  }
}
[11:44 a.m., 2024-12-13] Aarsh: Material design 

<mat-form-field>
  <mat-label>Cat Name</mat-label>
  <input matInput formControlName="name" />
</mat-form-field>

<mat-form-field>
  <mat-label>Cat Age</mat-label>
  <input matInput type="number" formControlName="age" />
</mat-form-field>

<mat-form-field>
  <mat-label>Cat Breed</mat-label>
  <input matInput formControlName="breed" />
</mat-form-field>

<button mat-raised-button color="primary" type="submit">
  Submit
</button>
