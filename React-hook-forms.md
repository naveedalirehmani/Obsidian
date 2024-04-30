```
"use client";

  

import React from "react";

import { useForm, Form, SubmitHandler } from "react-hook-form";

import { yupResolver } from "@hookform/resolvers/yup";

  

import { validationSchemaSignUp } from "@/lib/schemas";

  

type ReactHookFormProps = {};

  

interface formData {

firstName: string;

lastName: string;

age: number;

gender: "male" | "female";

email: string;

dateOfBirth: Date;

hobbies: string[];

password: string;

confirmPassword: string;

profilePicture: string;

}

  

const ReactHookForm = ({}: ReactHookFormProps): JSX.Element => {

const {

register,

reset, //* lets you reset form to a specific state.

setError, //* manually set error

setValue, //* manually set value

setFocus, //* manually set focus

getValues, //* get values of input of multiple

trigger, //* manually trigger validation

watch,

handleSubmit,

formState: {

errors, //* contains all fields that failed validation.

isDirty, //* field with modified default value.

dirtyFields, //* all fields that with modified value.

touchedFields, //* all fields that were touched ;)

defaultValues, //* defaul values.

isSubmitted, //* set true if onSubmit function executes with error.

isSubmitSuccessful, //* submit status.

isSubmitting, //* set to true will execution is in onSubmit body.

isLoading, //* we can set default values with a callback, set to true will callback is executing.

},

} = useForm({

defaultValues: {

firstName: "ayaz",

lastName: "datoo",

age: 19,

gender: "male",

email: "ayazdatoo@gmail.com",

dateOfBirth: new Date(1999, 8, 1),

hobbies: ["asdf","Asdf","Asdf","asdf"],

password: "password1A@",

confirmPassword: "password1A@",

profilePicture: "a;sldkjg;a",

},

mode: "onTouched", //* Validation strategy before submitting behaviour.

//! criteriaMode: 'all', //* Display all validation errors or one at a time.

shouldFocusError: true, //* When set to true (default), and the user submits a form that fails validation, focus is set on the first field with an error.

delayError: 500, //* adds delay in milliseconds before error display.

resolver: yupResolver(validationSchemaSignUp),

resetOptions: {

keepDirtyValues: true, //* user-interacted input will be retained

keepErrors: true, //* input errors will be retained with value update

},

});

  

const onSubmit: SubmitHandler<formData> = (values): void => {

console.log("submitted", values);

reset({});

};

  

console.log("errors", errors);

console.log("watch", watch()); //* watch all

// console.log("watch", watch(["firstName","lastName"])) //*watch only first and lastName.

// console.log("watch", watch("firstName")) //* watche specific field.

  

return (

<div className="min-h-screen flex items-center justify-center bg-gray-100">

<div className="max-w-md w-full bg-white p-6 rounded-md shadow-md">

<h2 className="text-2xl font-bold mb-6">Sign Up</h2>

<form onSubmit={handleSubmit(onSubmit as any)}>

{[

{ label: "First Name", type: "text", id: "firstName" },

{ label: "Last Name", type: "text", id: "lastName" },

{ label: "Age", type: "number", id: "age" },

{

label: "Gender",

type: "select",

id: "gender",

options: ["Male", "Female"],

},

{ label: "Email", type: "email", id: "email" },

{ label: "Date of Birth", type: "date", id: "dateOfBirth" },

{ label: "Hobbies", type: "text", id: "hobbies" },

{ label: "Password", type: "password", id: "password" },

{

label: "Confirm Password",

type: "password",

id: "confirmPassword",

},

{ label: "Profile Picture", type: "file", id: "profilePicture" },

].map(({ label, type, id, options }: any) => (

<div key={id} className="mb-4">

<label htmlFor={id} className="block text-gray-700">

{label}

</label>

{type === "select" ? (

<select

{...register(id)}

id={id}

className="w-full px-4 py-2 border rounded-md focus:outline-none focus:ring focus:border-blue-500"

>

<option value="">Select {label}</option>

{(options || [""]).map((option) => (

<option key={option} value={option.toLowerCase()}>

{option}

</option>

))}

</select>

) : (

<>

<input

{...register(id, {

setValueAs: (value) => {

return id === "age" ? parseInt(value) : value;

},

onBlur: (value) => {

console.log("onBlur", id, value);

},

})}

type={type}

// id={id}

className="w-full px-4 py-2 border rounded-md focus:outline-none focus:ring focus:border-blue-500"

/>

{errors[id] && (

<p className="text-red-500 animate-accordion-down">

{errors[id].message}

</p>

)}

</>

)}

</div>

))}

<div className="mt-6">

<button

type="submit"

className="w-full px-4 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 focus:outline-none"

>

Sign Up

</button>

</div>

</form>

</div>

</div>

);

};

  

export default ReactHookForm;
```