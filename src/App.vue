<template>
  <div>
    <FormProvider form="{this.form}">
      <SchemaField :key="schemaKey" :schema="schema"></SchemaField>
      <Submit type="primary" @submit="submit"> 提交 </Submit>
    </FormProvider>
  </div>
</template>

<script>
import { FormProvider, SchemaField } from "@formily/vue";
import { Submit } from "@formily/element-plus";

import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "App",
  components: {
    Submit,
  },
  setup() {
    const submit = () => {};

    const schemaKey = ref(null);
    const schema = {
      toolname: "波段拉伸",
      iconpath: "/img/tools/band_data_stretch.png",
      enable: true,
      op: "BandDataStrech",
      type: "N-1",
      formSchema: {
        type: "object",
        properties: {
          layout: {
            type: "void",
            "x-component": "FormLayout",
            "x-component-props": {
              labelCol: 6,
              wrapperCol: 10,
              layout: "vertical",
            },
          },

          output: {
            type: "object",
            "x-decorator": "FormGrid",
            "x-decorator-props": {
              // width: '100%',
              maxWidth: 100,
              strictAutoFit: true,
            },
            properties: {
              // 输出路径
              output_path: {
                type: "array",
                title: "输出文件",
                "x-decorator": "FormItem",
                "x-decorator-props": {
                  labelWidth: "200px",
                  gridSpan: "span 12",
                },
                // 默认值
                // default: [
                //     {
                //         fileName: '123',
                //         filePath: '123',
                //     },
                //     {
                //         fileName: '234',
                //         filePath: '234',
                //     },
                // ],
                "x-component": "Explorer",
                "x-component-props": {
                  baseUrl: "E://mnt//",
                  multiSelect: false,
                  value: [
                    {
                      fileName: "123",
                      filePath: "123",
                    },
                    {
                      fileName: "234",
                      filePath: "234",
                    },
                  ],
                },
                default: [],
              },
            },
          },
          title_config: {
            type: "void",
            "x-component": "NH3",
            "x-component-props": {
              prefix: "bar",
            },
            "x-content": "设置",
          },
          config: {
            type: "object",
            "x-decorator": "FormGrid",
            "x-decorator-props": {
              maxWidth: 100,
              strictAutoFit: true,
            },
            properties: {},
          },
        },
        // TODO:  这儿需要整清除ts的类型推断应该怎么用
        // NOTE:暂时用这种方式实现Formily的类型智能提醒
      },
    };
    return {
      submit,
      schemaKey,
      schema,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
