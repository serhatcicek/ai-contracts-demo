# Design System — Anar Rent A Car

All frontend implementations must use these design tokens for **Anar Rent A Car** branding.  
Changes to tokens must be reflected here before implementing in CSS/Tailwind config.

---

## Anar Branding

| Element | Value | Notes |
|---|---|---|
| **Company Name** | Anar Rent A Car | Professional, trustworthy |
| **Logo** | SVG mark + text | Orange primary + dark text |
| **Tagline** | Güvenilir Kiralama Çözümleri | "Reliable Rental Solutions" |
| **Primary Font** | Inter | Modern, clean, professional |
| **Language** | Turkish (tr-TR) | All content in Turkish |
| **Phone** | 0544 289 60 55 | Visible in header & footer |
| **Address** | Mardin, Turkey | Location-based branding |

---

## Color palette

| Token | Hex | Usage |
|---|---|---|
| `primary` | `#FF6B35` | Anar orange - Primary buttons, active states, links (Sixt-inspired) |
| `primary-dark` | `#E55A2B` | Anar orange dark - Button hover, emphasis |
| `primary-light` | `#FFE8DC` | Anar orange light - Subtle backgrounds, badges |
| `secondary` | `#1E293B` | Dark slate - Secondary actions, professional text |
| `accent` | `#00C4B4` | Turquoise - Highlights, price display, CTAs (contrast) |
| `danger` | `#DC2626` | Errors, destructive actions |
| `warning` | `#D97706` | Warnings |
| `success` | `#16A34A` | Success messages |
| `gray-50` | `#F9FAFB` | Page backgrounds |
| `gray-100` | `#F3F4F6` | Card backgrounds |
| `gray-200` | `#E5E7EB` | Borders |
| `gray-500` | `#6B7280` | Secondary text |
| `gray-700` | `#374151` | Body text |
| `gray-900` | `#111827` | Headings |
| `white` | `#FFFFFF` | |

---

## Typography

| Scale | Size | Weight | Usage |
|---|---|---|---|
| `text-xs` | 12px | 400 | Labels, captions |
| `text-sm` | 14px | 400 | Secondary text, form labels |
| `text-base` | 16px | 400 | Body text |
| `text-lg` | 18px | 500 | Sub-headings |
| `text-xl` | 20px | 600 | Card titles |
| `text-2xl` | 24px | 700 | Page section headings |
| `text-3xl` | 30px | 700 | Page titles |
| `text-4xl` | 36px | 800 | Hero headings |

Font family: `Inter, system-ui, sans-serif` (body); same for headings.

---

## Spacing

Use Tailwind's default 4px base spacing scale. Common patterns:
- Component padding: `p-4` (16px) or `p-6` (24px)
- Card gap: `gap-6` (24px)
- Section padding: `py-12` (48px) on desktop, `py-8` (32px) on mobile

---

## Border radius

| Token | Value | Usage |
|---|---|---|
| `rounded` | 4px | Inputs, small elements |
| `rounded-lg` | 8px | Cards |
| `rounded-xl` | 12px | Large cards, modals |
| `rounded-full` | 9999px | Badges, avatar chips |

---

## Shadows

| Token | Usage |
|---|---|
| `shadow-sm` | Subtle card lift |
| `shadow-md` | Hover state on cards |
| `shadow-lg` | Modals, dropdowns |

---

## Breakpoints (Tailwind defaults)

| Name | Min-width | Description |
|---|---|---|
| `sm` | 640px | Large phones |
| `md` | 768px | Tablets |
| `lg` | 1024px | Small desktops |
| `xl` | 1280px | Standard desktops |
| `2xl` | 1536px | Wide screens |

---

## Status badge colors

| Status | Background | Text |
|---|---|---|
| `available` | `green-100` | `green-800` |
| `rented` | `blue-100` | `blue-800` |
| `maintenance` | `yellow-100` | `yellow-800` |
| `inactive` | `gray-100` | `gray-500` |
| `pending` | `yellow-100` | `yellow-800` |
| `confirmed` | `green-100` | `green-800` |
| `cancelled` | `red-100` | `red-800` |
| `completed` | `gray-100` | `gray-600` |

---

## WhatsApp CTA button

- Background: `#25D366` (WhatsApp green)
- Text: white
- Icon: WhatsApp SVG icon before text
- Hover: darken 10%
- Label: "WhatsApp ile İletişim"
