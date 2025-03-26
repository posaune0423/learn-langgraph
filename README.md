# learn-langgraph

## How to run

```bash
pnpm install
tsx --env-file=.env src/basic/agent.ts
```

## 現在の疑問

1. `ChatPromptTemplate.fromMessages([])`とかの使い方がいまいちよくわからない、後内部でどういう型の解決をしてるのか、とか

```ts
ChatPromptTemplate.fromMessages([])
```

2. `StructuredOutputParser`もよくわからない

```ts
export const parser = StructuredOutputParser.fromZodSchema(
  z.object({
    proposal: tradeProposalSchema,
  })
)
```

3. `RunnableSequence.from([analyzerPrompt, gpt4oMini, parser])`の使い方がいまいちよくわからない、あと`invoke`の引数にいれる `formatInstructions` とか`ChatPromptTemplate`の型がどう関係しているのか

```ts
const chain = RunnableSequence.from([analyzerPrompt, gpt4oMini, parser])

const result = await chain.invoke({
  messages,
  formatInstructions: parser.getFormatInstructions(),
})
```

4. Node って特に LLM での入出力がないとだめな訳では無い？

```ts
import type { proposalAgentState } from '../utils/state'

// This node is just for connecting other data fetching nodes so that they can be called in parallel
export const dataFetchOperatorNode = async (
  state: typeof proposalAgentState.State
) => {
  console.log('dataFetchOperator', state)

  return state
}
```
