# Form array example

## component.ts
```ts
export class ToDoComponent implements OnInit {
    todoForm!: FormGroup
    todoArray!: FormArray

    constructor(private fb: FormBuilder) { }

    ngOnInit(): void {
        this.todoArray = this.fb.array([])
        this.todoForm = this.fb.group({ todos: this.todoArray })
    }

    addTodo() {
        const todoGroup = this.fb.group({
            date: this.fb.control<Date>(new Date()),
            description: this.fb.control<string>(''),
            priority: this.fb.control<string>('')
        })
        this.todoArray.push(todoGroup)
    }
}
```

## component.html

```html
<form [formGroup]="todoForm" (ngSubmit)="processForm()">
    <button type="button" (click)="addTodo()">Add TODO</button>
        <tbody formArrayName="todos">
            <tr *ngFor="let todo of todoArray.controls" [formGroup]="todo">
                <td><input type="date" formControlName="date"></td>
                <td><input type="text" formControlName="description"></td>
                <td>
                    <select formConntrolName="priority">
                        <option value="low">Low</option>
                        <option value="medium">Medium</option>
                        <option value="high">High</option>
                    </select>
                </td>
            </tr>
        </tbody>
    <button type="submit">Save</button>
</form>
```