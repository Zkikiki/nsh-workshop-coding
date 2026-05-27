# UI Event Notes

Use this reference when a UI button or interface instruction should trigger Creative Workshop code.

## Instruction vs Event

- 指令: used for UI-to-UI communication. A control sends an instruction, and other controls respond through custom properties on the client. Prefer this for simple interface presentation: show/hide controls, relay instructions, play UI animation, change opacity, position, scale, drag state, or switch visible UI layers.
- 事件: used for UI-to-code or UI-to-custom-ability communication. Use it only when Creative Workshop code or a custom ability must listen and run gameplay logic.

For pure UI behavior, do not convert the instruction into a code event. Configure the sending control and receiver controls directly:

1. Button property: click sends an interface instruction, such as `选框一`.
2. Receiver control custom property: `显示隐藏`, `发送指令`, animation, opacity, position, or scale responds to that instruction.
3. If one instruction should trigger more UI changes, add a `发送指令` custom property to relay it, such as receiving `选框一` and sending `关闭选框板` or `显框一`.

Use `发送事件` only when the instruction needs to cross into Creative Workshop code.

## Verified Button Instruction To Code Event Flow

Buttons send interface instructions first. To make Creative Workshop code receive a button action:

1. Configure the button property to send an interface instruction on click, such as `切换白噪音_风铃`.
2. In a control custom property, add `发送事件`.
3. Set `收到指令后` to the button instruction, such as `切换白噪音_风铃`.
4. In the `发送事件` field, open the event picker/dropdown and create or select the target event. Use the `创建新事件` entry when the event does not already exist.
5. In Creative Workshop code, listen with `收到事件` using that created/selected event.

Important: matching the instruction text by typing the same words is not enough if the event has not been created or selected in the event picker. If logs show the interface instruction but the `收到事件` block does not run, check event creation/selection before debugging code branches.

## Troubleshooting Checklist

- Confirm the button sends an interface instruction, not a code event directly.
- Confirm a visible or active control has a custom property that receives that instruction.
- Confirm the custom property action is `发送事件`, not `发送指令`.
- Confirm the event was created/selected from the event picker/dropdown, especially through `创建新事件`.
- Confirm the code uses `收到事件` for the same created event.
