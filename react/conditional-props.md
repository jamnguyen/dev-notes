## Conditional React Props

```ts
// Page.interface.ts

type ConditionalHeadingProps =
  | {
      withHeading?: true;
      title: string;
    }
  | {
      withHeading?: false;
      title?: never;
    };

export type PageProps = ConditionalHeadingProps & PropsWithChildren;


// Home.tsx

// Error!
<Page withHeading>Hello!</Page>

// Work!
<Page withHeading title="Home">Hello!</Page>

// Also work!
<Page>Hello!</Page>
```
