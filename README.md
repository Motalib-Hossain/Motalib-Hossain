## Table element

```
{
    field: 'task_status',
    header: 'Status',
    sortable: 'sortable',
    style: { width: '9%' },
    className: 'justify-center align-middle text-center',
},
```
## Form element

1. **Section**
2. **Field Configuration** (attribute type, name, id, class etc.)
3. **Flexible Field Types** (text, textarea, select, date, time)
4. **Validation Support** ( Custom validation , default validation(Min/max, required) )
5. **Layout Control**



```js
{
    task_subject: {
        field: "task_subject",
        label: "Subject",
        type: "input",
        required: false,
        className: "input"
    },
    task_description: {
        field: "task_description",
        label: "Description",
        type: "textarea",
        required: true,
        className: "textarea"
    }
}
```
---

## Static way 

```js

{createInfo?.task_subject?.type !== "hidden" && (
    <div className="input-group">
        <div className="lg:col-span-3">
            <label htmlFor={createInfo?.task_subject?.field} className="form-label">
                {createInfo?.task_subject?.label}
            </label>
        </div>
        <div className="lg:col-span-9">
            <input
                type={createInfo?.task_subject?.type}
                name={createInfo?.task_subject?.field}
                value={taskSave?.values?.task_subject || ""}
                onChange={taskSave?.handleChange}
                className={`form__control w-full py-2 ${createInfo?.task_subject?.className}`}
            />
        </div>
    </div>
)}

```


## Best way to re-present

```jsx
{
  type === "textarea" ? (
    <textarea
      name={value}
      required={required}
      maxLength={maxLength}
      minLength={minLength}
      className=""
    />
  ) : type === "select" ? (
    <select name={value} required={required} className="">
      <option value="">Select {label}</option>
      {/* Add options dynamically if available */}
    </select>
  ) : (
    <input
      type={type}
      name={value}
      required={required}
      maxLength={maxLength}
      minLength={minLength}
      className=""
    />
  );
}
```

---
## Controller

```Laravel get
$data = [];

    // Loop through each item in formConfig
    foreach ($formConfig as $field) {
        $data[] = [
            'create_' . $field['name'] . '_field' => $field['name'],
            'create_' . $field['name'] . '_label' => $field['label'],
            'create_' . $field['name'] . '_type' => $field['type'],
            'create_' . $field['name'] . '_required' => $field['required'] ? '1' : '0', // Convert boolean to '1' or '0'
            'create_' . $field['name'] . '_class' => $field['className'],
            'create_' . $field['name'] . '_icon' => $field['icon'],
            'create_' . $field['name'] . '_lengt_max' => (string) $field['maxLength'], // Convert to string
            'create_' . $field['name'] . '_length_min' => (string) $field['minLength'], // Convert to string
        ];
```
