## Conceptos y Uso en Remix

### Action
En Remix, una `action` es una función que se utiliza para manejar solicitudes POST en una ruta específica. Se define en el archivo de la ruta y se exporta como `action`. Esta función se utiliza para realizar operaciones como crear, actualizar o eliminar datos.

**Ejemplo:**
```tsx
export const action = async ({ request }: ActionFunctionArgs) => {
  const formData = await request.formData();
  const updates = Object.fromEntries(formData);
  await updateContact(params.contactId, updates);
  return redirect(`/contacts/${params.contactId}`);
};´´´

### Loader
Un loader en Remix es una función que se utiliza para cargar datos necesarios para renderizar una página. Se define en el archivo de la ruta y se exporta como loader. Esta función se ejecuta en el servidor antes de que la página se renderice.

export const loader = async () => {
  const contacts = await getContacts();
  return json({ contacts });
};

###useLoaderData
El hook useLoaderData se utiliza para acceder a los datos cargados por el loader en un componente de React. Este hook se llama dentro del componente y devuelve los datos cargados.

ejemploe: const { contacts } = useLoaderData<typeof loader>();


###useActionData
El hook useActionData se utiliza para acceder a los datos devueltos por una action después de que se haya enviado un formulario. Este hook se llama dentro del componente y devuelve los datos devueltos por la action.

ejemplo: const actionData = useActionData();

###Invariant
invariant es una función que se utiliza para realizar validaciones y lanzar errores si una condición no se cumple. Es útil para asegurarse de que ciertos valores o parámetros estén presentes antes de continuar con una operación.

Ejemplo: import invariant from "tiny-invariant";

export const loader = async ({ params }: LoaderFunctionArgs) => {
  invariant(params.contactId, "Missing contactId param");
  const contact = await getContact(params.contactId);
  if (!contact) {
    throw new Response("Not Found", { status: 404 });
  }
  return json({ contact });
};
