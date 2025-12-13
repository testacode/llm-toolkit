# Mantine Setup Reference

## Required Dependencies

```bash
npm install @mantine/core @mantine/hooks @mantine/form @mantine/notifications @mantine/modals
npm install @tabler/icons-react
npm install -D postcss postcss-preset-mantine postcss-simple-vars
```

## PostCSS Configuration

```javascript
// postcss.config.mjs
export default {
  plugins: {
    'postcss-preset-mantine': {},
    'postcss-simple-vars': {
      variables: {
        'mantine-breakpoint-xs': '36em',
        'mantine-breakpoint-sm': '48em',
        'mantine-breakpoint-md': '62em',
        'mantine-breakpoint-lg': '75em',
        'mantine-breakpoint-xl': '88em',
      },
    },
  },
};
```

## Provider Setup

```tsx
// src/providers/mantine-provider.tsx
'use client';

import { MantineProvider, createTheme } from '@mantine/core';
import { ModalsProvider } from '@mantine/modals';
import { Notifications } from '@mantine/notifications';

import '@mantine/core/styles.css';
import '@mantine/notifications/styles.css';

const theme = createTheme({
  primaryColor: 'blue',
  fontFamily: 'inherit',
});

type Props = {
  children: React.ReactNode;
};

export function MantineProviderWrapper({ children }: Props) {
  return (
    <MantineProvider theme={theme} defaultColorScheme="auto">
      <ModalsProvider>
        <Notifications position="top-right" />
        {children}
      </ModalsProvider>
    </MantineProvider>
  );
}
```

## Root Layout Integration

```tsx
// src/app/layout.tsx
import type { Metadata } from 'next';
import { ColorSchemeScript } from '@mantine/core';
import { MantineProviderWrapper } from '@/providers/mantine-provider';

export const metadata: Metadata = {
  title: 'App Name',
  description: 'App description',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" suppressHydrationWarning>
      <head>
        <ColorSchemeScript defaultColorScheme="auto" />
      </head>
      <body>
        <MantineProviderWrapper>
          {children}
        </MantineProviderWrapper>
      </body>
    </html>
  );
}
```

## Common Patterns

### Form with Validation

```tsx
import { useForm } from '@mantine/form';
import { TextInput, Button } from '@mantine/core';
import { z } from 'zod';
import { zodResolver } from 'mantine-form-zod-resolver';

const schema = z.object({
  email: z.string().email('Invalid email'),
  name: z.string().min(2, 'Name too short'),
});

function MyForm() {
  const form = useForm({
    mode: 'uncontrolled',
    initialValues: { email: '', name: '' },
    validate: zodResolver(schema),
  });

  return (
    <form onSubmit={form.onSubmit((values) => console.log(values))}>
      <TextInput
        label="Email"
        key={form.key('email')}
        {...form.getInputProps('email')}
      />
      <TextInput
        label="Name"
        key={form.key('name')}
        {...form.getInputProps('name')}
      />
      <Button type="submit">Submit</Button>
    </form>
  );
}
```

### Notifications

```tsx
import { notifications } from '@mantine/notifications';

// Success
notifications.show({
  title: 'Success',
  message: 'Operation completed',
  color: 'green',
});

// Error
notifications.show({
  title: 'Error',
  message: 'Something went wrong',
  color: 'red',
});
```

### Modals

```tsx
import { modals } from '@mantine/modals';

// Confirmation modal
modals.openConfirmModal({
  title: 'Confirm action',
  children: <p>Are you sure?</p>,
  labels: { confirm: 'Confirm', cancel: 'Cancel' },
  onConfirm: () => console.log('Confirmed'),
});
```
