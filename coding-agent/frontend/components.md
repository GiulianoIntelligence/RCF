# RCF - Front-end / Components

> Interactive UI components: things the user clicks, types into, or that animate in response to state. Reach for this file whenever the agent is about to build a discrete reusable widget.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Primary Button (shadcn/ui)

**Project fit:** Default action button for forms and CTAs in any Next.js / React app using shadcn/ui. Use when the action is the page's main intent (Submit, Save, Continue).

**Value:**

```tsx
import { Button } from "@/components/ui/button"

export function PrimaryButton({ children, ...props }: React.ComponentProps<typeof Button>) {
  return (
    <Button variant="default" size="default" {...props}>
      {children}
    </Button>
  )
}
```

---

## Context Relevancy: Destructive Button with confirm dialog (shadcn/ui)

**Project fit:** Any irreversible action - delete, archive, revoke, cancel-subscription. Wraps the button in an `AlertDialog` so the user must explicitly confirm. Use whenever a single click would otherwise destroy state.

**Value:**

```tsx
import { Button } from "@/components/ui/button"
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from "@/components/ui/alert-dialog"

export function DestructiveButton({
  label,
  onConfirm,
}: {
  label: string
  onConfirm: () => void
}) {
  return (
    <AlertDialog>
      <AlertDialogTrigger asChild>
        <Button variant="destructive">{label}</Button>
      </AlertDialogTrigger>
      <AlertDialogContent>
        <AlertDialogHeader>
          <AlertDialogTitle>Are you sure?</AlertDialogTitle>
          <AlertDialogDescription>This action cannot be undone.</AlertDialogDescription>
        </AlertDialogHeader>
        <AlertDialogFooter>
          <AlertDialogCancel>Cancel</AlertDialogCancel>
          <AlertDialogAction onClick={onConfirm}>Confirm</AlertDialogAction>
        </AlertDialogFooter>
      </AlertDialogContent>
    </AlertDialog>
  )
}
```

---

## Context Relevancy: Toast notification wrapper (sonner)

**Project fit:** App needs to surface success, error, and info feedback after async actions. Uses `sonner` for stacking, auto-dismiss, and theming. Wrap the project's only toast call sites in this `notify` helper so the API stays consistent.

**Value:**

```tsx
import { toast } from "sonner"

export const notify = {
  success: (msg: string) => toast.success(msg),
  error: (msg: string) => toast.error(msg),
  info: (msg: string) => toast(msg),
}
```

---

## Context Relevancy: Page-level error boundary (Next.js app router)

**Project fit:** Drop into `app/<segment>/error.tsx` to catch runtime errors thrown by server or client components in that route segment. Renders a recovery affordance via the `reset` prop. Required by Next.js for any route segment that ships to production.

**Value:**

```tsx
"use client"

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string }
  reset: () => void
}) {
  return (
    <div className="flex min-h-[60vh] flex-col items-center justify-center gap-4">
      <h2 className="text-xl font-semibold">Something went wrong.</h2>
      <button
        onClick={reset}
        className="rounded-md border px-4 py-2 text-sm hover:bg-muted"
      >
        Try again
      </button>
    </div>
  )
}
```

---

## Context Relevancy: Form with validation (react-hook-form + zod + shadcn/ui)

**Project fit:** Any form where field-level validation, type inference from schema, and shadcn-styled error messages matter. Replace the schema and `defaultValues` for each form; the wiring stays identical.

**Value:**

```tsx
"use client"

import { zodResolver } from "@hookform/resolvers/zod"
import { useForm } from "react-hook-form"
import { z } from "zod"
import { Button } from "@/components/ui/button"
import {
  Form,
  FormControl,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form"
import { Input } from "@/components/ui/input"

const schema = z.object({
  email: z.string().email(),
})

export function ExampleForm() {
  const form = useForm<z.infer<typeof schema>>({
    resolver: zodResolver(schema),
    defaultValues: { email: "" },
  })

  function onSubmit(values: z.infer<typeof schema>) {
    console.log(values)
  }

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField
          control={form.control}
          name="email"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Email</FormLabel>
              <FormControl>
                <Input placeholder="you@example.com" {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  )
}
```

---

## Context Relevancy: Modal / Dialog primitive

**Project fit:** App needs a focus-trapped, ESC-dismissable overlay for confirmations and short forms. Must lock background scroll and restore focus on close.

**Value:**

> _(Add your tested modal/dialog primitive here, including the open-state hook and any composition pattern - e.g. `<Dialog.Root><Dialog.Trigger/><Dialog.Content/></Dialog.Root>` - that the rest of your codebase relies on.)_
