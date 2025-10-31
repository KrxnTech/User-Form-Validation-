
# 🧾 Form Validation – Expense Tracker

### 📁 Feature Overview

The **Form Validation** feature ensures that users enter valid data before adding an expense.
It checks all input fields (Title, Amount, Category, Date), highlights any invalid input, and displays appropriate error or success messages.

---

## ⚙️ Elements Involved

| Variable                                                  | Description                                                       |
| --------------------------------------------------------- | ----------------------------------------------------------------- |
| `form`                                                    | The main expense form element                                     |
| `title`                                                   | Input field for expense title                                     |
| `amount`                                                  | Input field for expense amount                                    |
| `category`                                                | Input for expense category                                        |
| `date`                                                    | Input for date of expense                                         |
| `addExpenseButton`                                        | Button to trigger validation and add an expense                   |
| `titleError`, `amountError`, `categoryError`, `dateError` | Error message containers for invalid inputs                       |
| `success`                                                 | Success message container displayed when all fields are valid     |
| `ADD`                                                     | Dynamically created div that shows “Expense Added Successfully ✅” |

---

## 🧠 Validation Flow

### Step-by-step Logic:

1. **User clicks "Add Expense"**

   * Triggers the event listener on `addExpenseButton`.

2. **clearError()**

   * Hides all previous error or success messages.
   * Resets all input borders to default (`2px solid black`).

3. **Input Validation Checks**

   * Each field is checked in order:

     1. Empty **Title** → shows red border & error message
     2. Invalid **Title** (contains numbers/symbols) → regex error
     3. Empty **Amount** → error
     4. Amount ≤ 0 → error
     5. Empty **Category** → error
     6. Empty **Date** → error

4. **If all inputs valid:**

   * Show `success` message.
   * Call `storeExpense()` to save expense.
   * Call `celebration()` to display confirmation message.
   * Call `clearForm()` to reset all input fields.

---

## 🔁 Function Call Order

| Order | Function                | Purpose                                        |
| ----- | ----------------------- | ---------------------------------------------- |
| 1️⃣   | `clearError()`          | Reset old errors and input borders             |
| 2️⃣   | Inline `if` validations | Validate all form inputs                       |
| 3️⃣   | `storeExpense()`        | Save expense data to local storage             |
| 4️⃣   | `celebration()`         | Display “Expense Added Successfully ✅” message |
| 5️⃣   | `clearForm()`           | Clear all input fields                         |

---

## 🧩 Functions Explained

### **1. clearError()**

Resets UI before validation.

```js
function clearError() {
    titleError.style.display = "none";
    amountError.style.display = "none";
    categoryError.style.display = "none";
    dateError.style.display = "none";
    success.style.display = "none";
    title.style.border = "2px solid black";
    amount.style.border = "2px solid black";
    category.style.border = "2px solid black";
    date.style.border = "2px solid black";
    ADD.style.display = "none";
}
```

---

### **2. celebration()**

Displays a temporary success message after successful form submission.

```js
function celebration() {
    ADD.style.display = "block";
}
```

---

### **3. clearForm()**

Clears all input fields after successful form submission.

```js
function clearForm() {
    title.value = "";
    amount.value = "";
    category.value = "";
    date.value = "";
}
```

---

### **4. Event Listener**

Main trigger for validation.

```js
addExpenseButton.addEventListener("click", () => {
    const titleValue = title.value.trim();
    const regex = /^[A-Za-z\s]+$/;
    clearError();

    if (title.value == "") {
        titleError.style.display = "block";
        title.style.border = "2px solid red";
    }
    else if (!regex.test(titleValue)) {
        titleError.style.display = "block";
        titleError.textContent = "Title must contain only letters";
    }
    else if (amount.value == "") {
        amountError.style.display = "block";
        amount.style.border = "2px solid red";
    }
    else if (amount.value <= 0) {
        amountError.style.display = "block";
        amountError.textContent = "Amount must be greater than 0";
    }
    else if (category.value == "") {
        categoryError.style.display = "block";
        category.style.border = "2px solid red";
    }
    else if (date.value == "") {
        dateError.style.display = "block";
        date.style.border = "2px solid red";
    }
    else {
        success.style.display = "block";
        storeExpense();
        celebration();
        clearForm();
    }
});
```

---

## 🔍 Visual Flow Diagram

```mermaid
flowchart TD

A[User Clicks 'Add Expense'] --> B[clearError()]
B --> C[Check Title Empty?]
C -->|Yes| E1[Show Title Error & Red Border]
C -->|No| D[Check Title Valid (Regex)]
D -->|Invalid| E2[Show "Only letters allowed"]
D -->|Valid| F[Check Amount Empty?]
F -->|Yes| E3[Show Amount Error]
F -->|No| G[Check Amount <= 0?]
G -->|Yes| E4[Show 'Amount > 0' Error]
G -->|No| H[Check Category Empty?]
H -->|Yes| E5[Show Category Error]
H -->|No| I[Check Date Empty?]
I -->|Yes| E6[Show Date Error]
I -->|No| J[Valid Input → Success Flow]
J --> K[Display Success Message]
K --> L[storeExpense()]
L --> M[celebration()]
M --> N[clearForm()]
N --> O[End]
```

---

## ✅ Summary

| Feature              | Description                                        |
| -------------------- | -------------------------------------------------- |
| **Purpose**          | Prevents invalid inputs before saving expense data |
| **Validation Type**  | Manual, using `if-else` and regex                  |
| **Error Feedback**   | Red border + visible error message                 |
| **Success Feedback** | “Expense Added Successfully ✅” message             |
| **Final Actions**    | Save → Celebrate → Reset Form                      |

---

Alright, Halsar, now we’re talking in diagrams instead of brain fog. Let’s build a **complete ladder-style breakdown** (like a blueprint) showing *how the whole Form Validation system is constructed*, what’s required, and how each piece connects.

This is your **Form Validation Architecture Map** — basically, how all the parts talk to each other.

---

# 🧩 FORM VALIDATION LADDER (Expense Tracker)

### 🎯 Goal:

To validate all form inputs (title, amount, category, date), show error messages for invalid data, and show success + store valid data when everything checks out.

---

## 🪜 STEP-BY-STEP LADDER

```
                ┌────────────────────────────────────┐
                │  START: User clicks “Add Expense”  │
                └────────────────────────────────────┘
                                │
                                ▼
        ┌──────────────────────────────────────────────┐
        │ 1️⃣ CALL clearError()                        │
        │ → Hides old error messages                   │
        │ → Resets borders to black                    │
        │ → Hides success message                      │
        └──────────────────────────────────────────────┘
                                │
                                ▼
        ┌──────────────────────────────────────────────┐
        │ 2️⃣ FETCH INPUT VALUES                        │
        │ title.value.trim(), amount.value, etc.        │
        │ regex = /^[A-Za-z\s]+$/                      │
        └──────────────────────────────────────────────┘
                                │
                                ▼
        ┌──────────────────────────────────────────────┐
        │ 3️⃣ VALIDATION CHAIN                          │
        │ → if title empty → show titleError            │
        │ → else if title invalid (regex) → show error  │
        │ → else if amount empty → show amountError     │
        │ → else if amount ≤ 0 → show error             │
        │ → else if category empty → show error         │
        │ → else if date empty → show error             │
        └──────────────────────────────────────────────┘
                                │
                  ┌─────────────┴─────────────┐
                  ▼                           ▼
      ┌────────────────────┐      ┌────────────────────────────┐
      │ ❌ INVALID INPUT    │      │ ✅ VALID INPUT              │
      │ → Shows red border  │      │ → Shows success message    │
      │ → Shows error text  │      │ → Calls:                   │
      │                    │      │   - storeExpense()          │
      │                    │      │   - celebration()           │
      │                    │      │   - clearForm()             │
      └────────────────────┘      └────────────────────────────┘
                                              │
                                              ▼
                     ┌────────────────────────────────────────┐
                     │ 4️⃣ storeExpense()                     │
                     │ → Creates expense object (id, title...) │
                     │ → Pushes to expense array               │
                     │ → Saves to localStorage                 │
                     │ → Calls displayExpense()                │
                     │ → Calls SHOW_TOTAL_NUMBER_OF_CATEGORIES()│
                     └────────────────────────────────────────┘
                                              │
                                              ▼
                     ┌────────────────────────────────────────┐
                     │ 5️⃣ celebration()                      │
                     │ → Shows success div “Expense Added ✅” │
                     └────────────────────────────────────────┘
                                              │
                                              ▼
                     ┌────────────────────────────────────────┐
                     │ 6️⃣ clearForm()                        │
                     │ → Empties all input fields              │
                     └────────────────────────────────────────┘
```

---

## 🧱 COMPONENTS REQUIRED

| Component                                | Type    | Purpose                                             |
| ---------------------------------------- | ------- | --------------------------------------------------- |
| **HTML Form**                            | UI      | Holds all input fields & submit button              |
| **Error Messages (`<p id="...Error">`)** | UI      | To display specific validation errors               |
| **Success Message (`#success`)**         | UI      | Displays when form is valid                         |
| **CSS Defaults**                         | Styling | Initially hides errors & sets default border color  |
| **JS Functions**                         | Logic   | Handle validation, cleaning, storing, and resetting |
| **Local Storage**                        | Data    | Saves expense entries for persistence               |

---

## 🔗 FUNCTION CONNECTION MAP

```
[User Click]
   │
   ▼
[Event Listener → Validation Start]
   │
   ├─► clearError()
   │
   ├─► (if conditions)
   │     ├─ show error (titleError, amountError…)
   │     └─ stop further execution if invalid
   │
   └─► (else block if valid)
         ├─ success.style.display = "block"
         ├─ storeExpense()
         │     ├─ displayExpense()
         │     └─ SHOW_TOTAL_NUMBER_OF_CATEGORIES()
         ├─ celebration()
         └─ clearForm()
```

---

## 🧠 How Functions Talk To Each Other

| Function           | Called By                              | Purpose                    | Calls Further                                       |
| ------------------ | -------------------------------------- | -------------------------- | --------------------------------------------------- |
| **clearError()**   | addExpenseButton click                 | Reset UI before validation | —                                                   |
| **storeExpense()** | addExpenseButton click (on valid form) | Save data to localStorage  | displayExpense(), SHOW_TOTAL_NUMBER_OF_CATEGORIES() |
| **celebration()**  | addExpenseButton click (on valid form) | Display “Success ✅” div    | —                                                   |
| **clearForm()**    | addExpenseButton click (on valid form) | Empty all input fields     | —                                                   |

---

## 🎨 Visual Node Connection Diagram

```mermaid
graph TD

A[User Clicks Add Expense] --> B(clearError)
B --> C{Input Validation Checks}
C -->|Invalid| D[Show Error + Red Border]
C -->|Valid| E[Show Success Message]
E --> F[storeExpense()]
F --> F1[displayExpense()]
F --> F2[SHOW_TOTAL_NUMBER_OF_CATEGORIES()]
E --> G[celebration()]
E --> H[clearForm()]
```

---

## ✅ Summary

* **clearError()** always runs first to reset UI.
* **Validation checks** control which message shows.
* **On valid input**, data is stored, form cleared, and user notified.
* The process restarts cleanly on the next click.

---

Would you like me to generate a **visual PNG flowchart** version of this ladder (like a real diagram you can add to your documentation file)? It’ll look neat in your project README.

