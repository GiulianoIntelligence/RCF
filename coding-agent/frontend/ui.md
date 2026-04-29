# RCF - Front-end / UI

> Layout primitives, design-system shells, and structural pieces that wrap pages or sections. The agent should consult this file before scaffolding any layout-level UI.

See [`SYSTEM_PROMPT.md`](../../SYSTEM_PROMPT.md) for how the agent picks an entry from this file.

---

## Context Relevancy: Sidebar layout (shadcn/ui, collapsible, app-router)

**Project fit:** Next.js / React app using shadcn/ui's `sidebar` primitive. Use as the root layout when the app needs a persistent collapsible left navigation with a `SidebarTrigger` in the main pane.

**Value:**

```tsx
import { SidebarProvider, SidebarTrigger } from "@/components/ui/sidebar"
import { AppSidebar } from "@/components/app-sidebar"

export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <SidebarProvider>
      <AppSidebar />
      <main>
        <SidebarTrigger />
        {children}
      </main>
    </SidebarProvider>
  )
}
```

---

## Context Relevancy: Page header with breadcrumbs

**Project fit:** Internal/admin pages where users need orientation across nested routes. Pair with the sidebar layout above.

**Value:**

> _(Add your tested page-header + breadcrumb component here. Until then, this is an RCF miss and the agent should generate.)_
