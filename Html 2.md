Great. Let's continue with Part 2, which focuses on HTML Forms. Forms are one of the most frequently tested topics in interviews for both frontend and full-stack roles.

HTML Interview Guide – Part 2 (HTML Forms)


---

Q21. What is an HTML Form?

Answer

An HTML form is used to collect user input and send it to a server for processing.

Examples of user input include:

Username

Password

Email

Phone number

Feedback

Payment details


Syntax

<form>
    <!-- Form elements go here -->
</form>

Example

<form>
    <label>Name:</label>
    <input type="text">

    <button>Submit</button>
</form>

Step-by-Step Explanation

Step 1: <form> creates the form container.

Step 2: <label> describes the purpose of the input.

Step 3: <input> accepts user input.

Step 4: <button> submits the form.


---

Q22. What is the action attribute?

Answer

The action attribute specifies where the form data is sent after submission.

Example

<form action="/login">
    <input type="text">
    <button>Submit</button>
</form>

Flow

User fills form
       ↓
Clicks Submit
       ↓
Browser sends data
       ↓
/login endpoint

Without an action, the form is typically submitted to the current page URL.


---

Q23. What is the method attribute?

Answer

The method attribute specifies how the data is sent.

Two common values are:

GET

POST



---

GET Method

Example

<form action="/search" method="get">

Characteristics

Appends data to the URL.

Suitable for retrieving data.

Can be bookmarked.

Not suitable for sensitive information.


Example URL

/search?name=John


---

POST Method

Example

<form action="/login" method="post">

Characteristics

Sends data in the request body.

Better for sensitive information.

No practical URL length limitation like GET.

Used for creating or updating data.



---

Interview Comparison

GET	POST

Retrieves data	Sends data
Data in URL	Data in request body
Can be bookmarked	Cannot be bookmarked with submitted data
Less suitable for sensitive data	Better for sensitive data
Can be cached	Usually not cached by default



---

Q24. Explain the <input> element.

Answer

The <input> element is used to collect different types of user input.

Syntax

<input type="text">

The type attribute determines the behavior.


---

Q25. What are different input types?

Some common input types are:

<input type="text">

<input type="password">

<input type="email">

<input type="number">

<input type="date">

<input type="time">

<input type="file">

<input type="checkbox">

<input type="radio">

<input type="color">

<input type="range">

<input type="search">

<input type="tel">

<input type="url">

<input type="hidden">

<input type="submit">

<input type="reset">


---

Q26. Explain type="text"

<input type="text">

Used for general text input.

Example

<input type="text" placeholder="Enter your name">

Output

____________________


---

Q27. Explain type="password"

<input type="password">

Characters are masked.

Example

<input type="password">

Display

••••••••

Interview Tip: The browser masks the characters, but this alone does not encrypt the password. Secure transmission depends on using HTTPS.


---

Q28. Explain type="email"

<input type="email">

Checks whether the entered value looks like an email address before form submission.

Example

<input type="email">

Valid

abc@gmail.com

Invalid

abcgmail.com


---

Q29. Explain type="number"

<input type="number">

Accepts numeric values.

Example

<input
    type="number"
    min="1"
    max="100">

Only values between 1 and 100 are allowed by the browser's validation.


---

Q30. Explain type="date"

<input type="date">

Provides a date picker.

Example

<input type="date">

Typical Output

📅 2026-06-26


---

Q31. Explain type="file"

<input type="file">

Allows users to choose files from their device.

Example

<input type="file">

To upload multiple files:

<input type="file" multiple>


---

Q32. Difference between Radio Button and Checkbox

Radio Button

<input type="radio">

Only one option can be selected within a group (same name).

Example

<input type="radio" name="gender"> Male

<input type="radio" name="gender"> Female


---

Checkbox

<input type="checkbox">

Allows selecting multiple options.

Example

<input type="checkbox"> HTML

<input type="checkbox"> CSS

<input type="checkbox"> JavaScript


---

Comparison

Radio	Checkbox

One selection	Multiple selections
Circular control	Square control
Same name groups choices	Each box is independent unless handled otherwise



---

Q33. What is the <label> element?

Answer

The <label> element provides a caption for a form control.

Example

<label for="email">Email</label>

<input id="email" type="email">

Benefits

Better accessibility.

Clicking the label focuses the associated input.

Easier to use on touch devices.



---

Q34. Difference between id and name in forms

id

Used for:

CSS

JavaScript

Associating <label> with a form control


Example

<input id="username">


---

name

Used when submitting form data.

Example

<input
    name="username">

Submitted as:

username=John


---

Comparison

id	name

Identifies the element in the page	Identifies the submitted form field
Must be unique	Can be reused in some cases (for example, radio groups)
Used by labels, CSS, JavaScript	Used in form submission



---

Q35. What is the placeholder attribute?

Shows a hint inside an input before the user enters data.

Example

<input
    type="text"
    placeholder="Enter your name">

Display

Enter your name

The placeholder disappears when the user starts typing. It is not a replacement for a <label> because placeholders may not always be visible and are not a reliable accessible label.


---

Q36. What is the required attribute?

Makes a field mandatory.

Example

<input
    type="email"
    required>

If the field is empty, the browser prevents submission and prompts the user to fill it in.


---

Q37. What are readonly and disabled?

readonly

<input
    value="John"
    readonly>

User cannot edit the value.

The value is still submitted with the form.



---

disabled

<input
    value="John"
    disabled>

User cannot interact with the control.

The value is not submitted with the form.



---

Comparison

Readonly	Disabled

Cannot edit	Cannot interact
Submitted	Not submitted
Can receive focus (depending on browser)	Typically cannot receive focus



---

Q38. What is the <textarea> element?

Used for multi-line text input.

Example

<textarea
rows="4"
cols="30">
</textarea>

Commonly used for:

Comments

Feedback

Messages

Descriptions



---

Q39. What is the <select> element?

Creates a drop-down list.

Example

<select>
    <option>India</option>
    <option>USA</option>
    <option>Japan</option>
</select>

Output

▼ India


---

Q40. Difference between <button> and <input type="submit">

<button>

<button>Login</button>

Can contain text, icons, or HTML.

More flexible.


<input type="submit">

<input
type="submit"
value="Login">

Simpler.

Displays only the value as text.


Interview Answer

<button> is generally preferred because it supports richer content and is more flexible for styling and accessibility when used correctly.


Extra:::::
Yes, but there's an important difference in React.

For form elements like <input>, <select>, and <textarea>, you usually use onChange.

Input

function App() {
  const handleChange = (e) => {
    console.log(e.target.value);
  };

  return <input type="text" onChange={handleChange} />;
}

Select

function App() {
  const handleSelect = (e) => {
    console.log(e.target.value);
  };

  return (
    <select onChange={handleSelect}>
      <option>HTML</option>
      <option>CSS</option>
      <option>React</option>
    </select>
  );
}

Checkbox

<input
  type="checkbox"
  onChange={(e) => console.log(e.target.checked)}
/>

Radio

<input
  type="radio"
  name="gender"
  value="Male"
  onChange={(e) => console.log(e.target.value)}
/>

onSelect in React

onSelect is not used for dropdown (<select>) elements. It is triggered when the user selects (highlights) text inside an <input> or <textarea>.

<input
  type="text"
  onSelect={() => console.log("Text selected")}
/>

Remember:

✅ onChange → Use for <input>, <select>, <textarea>, checkbox, and radio.

✅ onSelect → Use when detecting text selection, not dropdown selection.


---

Frequently Asked Form Interview Questions

1. What is the difference between GET and POST?


2. Why do we use the name attribute?


3. Why is a <label> important?


4. What is the difference between readonly and disabled?


5. Can a form work without the action attribute?


6. Why use required?


7. How do radio buttons differ from checkboxes?


8. Which input types provide built-in browser validation?


9. Why shouldn't placeholder replace a <label>?


10. What is the purpose of the method attribute?



In Part 3, we'll cover Semantic HTML, HTML5 elements, SEO, Accessibility (ARIA), and advanced interview questions, which are very common in interviews for experienced frontend developers.
