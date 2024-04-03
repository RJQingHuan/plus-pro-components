# 基础 Ts 类型

::: tip 提示

本页面类型会互相引用，请注意上下文!

:::

## ElementRefType

ref 绑定的元素类型

```ts
/**
 * ref 绑定的元素类型
 */
export type ElementRefType = HTMLElement | null
```

## Timeout

setTimeout 类型

```ts
/**
 * setTimeout 类型
 */
export type Timeout = ReturnType<typeof setTimeout>
```

## Interval

setInterval 类型

```ts
/**
 * setInterval 类型
 */
export type Interval = ReturnType<typeof setInterval>
```

## RecordType

普通的对象的泛型

```ts
/**
 * 普通的对象的泛型
 */
export type RecordType = {
  [index: string]: any
}
```

## Nullable

允许 null 的泛型

```ts
/**
 * 允许null的泛型
 */
export type Nullable<T> = T | null
```

## Mutable

去除只读状态

```ts
/**
 * 去除只读状态
 */
export type Mutable<T extends Record<string, any>> = {
  -readonly [K in keyof T]: T[K]
}
```

## PageInfo

分页参数

```ts
/**
 * 分页参数
 */
export interface PageInfo {
  /**
   * 默认为1
   */
  page: number
  /**
   * 默认为10
   */
  pageSize: number
}
```

## ActionBarButtonsRow

表格操作栏按钮配置项的值的类型

```ts
import type { ElMessageBoxOptions } from 'element-plus'
import type { Component, Ref, ComputedRef, AppContext } from 'vue'
import type { RecordType, ButtonsCallBackParams } from 'plus-pro-components'
/**
 * 表格操作栏按钮配置项的值的类型
 */
export interface ActionBarButtonsRow {
  /**
   * 操作文本
   */
  text: string
    | Ref<string>
    | ComputedRef<string>
    | ((row: any, index: number, button: ActionBarButtonsRow) => string | Ref<string> | ComputedRef<string>)
  /**
   * 操作唯一code
   *
   */
  code?: string | number

  /**
   * 禁用
   */
  disabled?: boolean

  /**
   * `@element-plus/icons-vue` 的图标名称，对ElButton,ElLink 和ElIcon 组件同时生效
   */
  icon?: Component
  /**
   * ElButton,ElLink和ElIcon 组件对应的props
   */
  props?: RecordType
  /**
   * ElTooltip组件的props， type 为icon 时生效
   */
  tooltipProps?: RecordType

  /**
   * 按钮显示的逻辑 默认 true 显示， 不需要显示给 false
   *
   * 可以用来控制权限
   */
  show?:
    | boolean
    | Ref<boolean>
    | ComputedRef<boolean>
    | ((
        row: any,
        index: number,
        button: ActionBarButtonsRow
      ) => boolean | Ref<boolean> | ComputedRef<boolean>)

  /**
   * 操作是不是需要二次确认  默认值为 `false`
   */
  confirm?:
    | boolean
    | {
        /**
         * 默认 `提示`
         */
        title?: string | ((data: ButtonsCallBackParams) => string)
        /**
         * 默认 `确定执行本次操作`
         */
        message?: string | ((data: ButtonsCallBackParams) => string)
        /**
         *  ElMessageBox.confirm的 options
         */
        options?: ElMessageBoxOptions

        /**
         *  ElMessageBox.confirm的 appContext
         */
        appContext?: AppContext | null
      }
}
```

## ActionBarProps

表格操作栏数据类型

```ts
import type { ActionBarButtonsRow } from 'plus-pro-components'

/**
 * 表格操作栏数据类型
 */
export interface ActionBarProps {
  /**
   * 操作栏名称  默认值为 `'操作栏'`
   *
   */
  label?: string
  /**
   * 操作栏固定   默认值为 `'right'`
   */
  fixed?: string
  /**
   * 显示出来的按钮个数  默认值为 `3`
   */
  showNumber?: number
  /**
   * 操作按钮的类型   默认值为 `'link'`
   */
  type?: 'icon' | 'button' | 'link'
  /**
   * 操作按钮集合   默认值为 `[]`
   */
  buttons?: ActionBarButtonsRow[]
  /**
   * 表格操作栏 el-table-column 的其width   默认值为 `200`
   */
  width?: string | number
  /**
   * 表格操作栏 el-table-column 的其他props   默认值为 `{}`
   */
  actionBarTableColumnProps?: Partial<import('element-plus')['TableColumnCtx']>
}
```

## TableFormRefRow

表格可编辑表单的行 form 的参数类型

```ts
import { ElForm, ElFormItem } from 'element-plus'
import type { Ref } from 'vue'

/**
 * 表格可编辑表单的行form 的参数类型
 */
export interface TableFormRefRow {
  /**
   * 单元格的表单实例
   */
  formInstance: Ref<InstanceType<typeof ElForm>>
  /**
   * 表格的行索引
   */
  index: number
  /**
   * 表格的列字段
   */
  prop: string
  /**
   * 单元格的表单开启编辑
   * @returns
   */
  startCellEdit: () => void
  /**
   * 单元格的表单停止编辑
   * @returns
   */
  stopCellEdit: () => void
}
```

## ButtonsCallBackParams

表格点击按钮回调的参数的类型

```ts
import type { RecordType, buttonsKeyRow, TableFormRefRow } from 'plus-pro-components'

/**
 * 表格点击按钮回调的参数的类型
 */
export interface ButtonsCallBackParams {
  /**
   * 表格行数据
   */
  row: RecordType
  /**
   * 点击按钮数据
   */
  buttonRow: buttonsKeyRow
  /**
   * 表格索引
   */
  index: number
  /**
   * 按钮点击事件数据
   */
  e: MouseEvent
  /**
   * 可编辑表单的行form
   */
  formRefs?: TableFormRefRow[]
}
```

## TableValueType

所有表格列显示的类型 默认是 `undefined`

```ts
/**
 * 所有表格列显示的类型 默认是 `undefined`
 */
export type TableValueType =
  | 'img'
  | 'link'
  | 'money'
  | 'tag'
  | 'progress'
  | 'copy'
  | 'code'
  | undefined
```

## FormItemValueType

所有表单的类型 默认是 `input` (`undefined`)

```ts
/**
 * 所有表单的类型 默认是 `input` (`undefined`)
 */
export type FormItemValueType =
  | 'autocomplete'
  | 'cascader'
  | 'checkbox'
  | 'color-picker'
  | 'date-picker'
  | 'input-number'
  | 'radio'
  | 'rate'
  | 'select'
  | 'slider'
  | 'switch'
  | 'time-picker'
  | 'time-select'
  | 'textarea'
  | 'input'
  | 'text'
  | 'plus-radio'
  | 'plus-date-picker'
  | 'plus-input-tag'
  | undefined
```

## FieldValueType

单个表单值的类型

```ts
/**
 * 单个表单值的类型
 */
export type FieldValueType =
  | string
  | number
  | boolean
  | null
  | undefined
  | Date
  | string[]
  | number[]
  | boolean[]
  | Date[]
  | [Date, Date]
  | [number, number]
  | [string, string]
```

## FieldValues

整体表单值的类型

```ts
import type { FieldValueType } from 'plus-pro-components'

/**
 * 整体表单值的类型
 */
export type FieldValues = Record<string, FieldValueType>
```

## PropsItemType

自定义 props 类型

```ts
import type { FieldValueType } from 'plus-pro-components'
/**
 *  自定义props类型  值支持对象 object，computed，函数和 Promise。
 */
export type PropsItemType<T extends Record<string, any> = any> =
  | Partial<T>
  | ComputedRef<Partial<T>>
  | ((
      value: FieldValueType,
      data: {
        row: Record<string, any>
        index: number
      }
    ) => Partial<T> | Promise<Partial<T>>)
  | Promise<Partial<T>>
```

## OptionsRow

选择框类型

```ts
import type { PropsItemType, RecordType } from 'plus-pro-components'
/**
 * 选择框类型
 */
export interface OptionsRow {
  label: number | string
  value: number | string
  /**
   * 小圆点背景色，
   * color 优先级 高于 type
   */
  color?: string
  /**
   * 小圆点背景色，
   * type 优先级 低于 color，
   * 只支持 'success' | 'warning' | 'info' | 'primary' | 'danger'
   */
  type?: Exclude<ButtonType, 'default' | 'text' | ''>
  /**
   * 表单子项的props  如 el-checkbox-group下的el-checkbox的props
   */
  fieldItemProps?: RecordType
  /**
   * el-checkbox-group下的，每一项el-checkbox的各自插槽(即el-checkbox的default插槽)。
   * el-radio-group下的，每一项el-checkbox的内容各自插槽(即el--radio的default插槽)。
   *
   * @see https://element-plus.org/zh-CN/component/checkbox.html#checkbox-slots
   * @see https://element-plus.org/zh-CN/component/radio.html#radio-slots
   */
  fieldSlot?: (option?: OptionsRow) => VNode | string
  /**
   * 子选项
   */
  children?: OptionsRow[]
}
```

## OptionsType

选择类型

```ts
import type { OptionsRow } from 'plus-pro-components'
/**
 * 选择类型   支持数组，computed，函数和Promise
 */
 */
export type OptionsType =
  | OptionsRow[]
  | ComputedRef<OptionsRow[]>
  | ((props?: PlusColumn) => OptionsRow[] | Promise<OptionsRow[]>)
  | Promise<OptionsRow[]>
```

## PlusFormGroupRow

分步表单配置项

```ts
import type { Component } from 'vue'
import type { PlusColumn } from 'plus-pro-components'

/**
 * 分组表单配置项
 */
export interface PlusFormGroupRow {
  title: string
  icon?: Component
  columns: PlusColumn[]
}
```

## PlusStepFrom

分步表单配置项

```ts
import type { Component } from 'vue'
import type { PlusFormProps } from 'plus-pro-components'

/**
 * 分步表单配置项
 */
export interface PlusStepFrom {
  title: string
  description?: string
  icon?: string | Component
  status?: '' | 'wait' | 'process' | 'finish' | 'error' | 'success'
  form: PlusFormProps
}
```

## TitleBar

表格标题栏

```ts
import type { Options as SortableOptions } from 'sortablejs'

/**
 * 标题栏
 */
export type TitleBar = {
  /**
   * 标题  使用title插槽则此配置不生效
   */
  title?: string

  /**
   *  是否需要刷新  默认false
   */
  refresh?: boolean

  /**
   *  是否需要密度控制  默认true
   */
  density?: boolean
  /**
   * 是否需要列设置 默认true
   */
  columnSetting?: boolean | { dragSort?: boolean | Partial<SortableOptions> }

  /**
   * 工具栏 icon 的大小和颜色配置
   */
  icon?: {
    /**
     * icon 的大小  默认 18
     */
    size?: string
    /**
     * icon 的颜色  默认 #606266
     */
    color?: string
  }
}
```

## PlusRouteRecordRaw

扩展的路由类型

```ts
import type { RouteRecordRaw } from 'vue-router'
import type { VNode, Component } from 'vue'
/**
 * 路由配置类型
 *
 * @description 继承自 vue-router 的 RouteRecordRaw，无侵入，仅仅只扩展 meta，meta除了扩展的属性外，同时支持添加任意自定义属性，
 * 外链的话  path给   '/'+链接   例： `/https://element-plus.org`
 *
 */
export type PlusRouteRecordRaw = Partial<Omit<RouteRecordRaw, 'children'>> & {
  /**
   * meta除了扩展的属性外，同时支持添加任意自定义属性
   *
   */
  meta?: {
    /**
     * 页面标题   标题存在面包屑和菜单名称显示标题  不存在显示路由的 name  name不存在显示路由的 path
     */
    title?: string
    /**
     * 图标
     */
    icon?: Component | VNode | ((route: PlusRouteRecordRaw) => VNode)
    /**
     * 排序，默认为0 只对第一级有效
     */
    sort?: number
    /**
     * 在侧边栏菜单中隐藏，默认false 不隐藏
     */
    hideInMenu?: boolean
    /**
     * 隐藏面包屑，默认false 不隐藏
     */
    hideInBreadcrumb?: boolean
    /**
     * 菜单是否禁用
     * @see https://element-plus.org/zh-CN/component/menu.html#menu-item-attributes
     */
    disabled?: boolean
  }
  children?: PlusRouteRecordRaw[]
}
```
