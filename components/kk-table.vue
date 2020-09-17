<template>
    <div class="table-wrapper">
        <table class="table" :class="{border, stripe}">
            <!-- 表头 -->
            <thead>
                <tr>
                    <th><input type="checkbox" :checked="isAllChecked" @change="(e) => selectedAllChange(e)" ref="allCheckbox"></th>
                    <th v-for="column in columns" :key="column.key">{{column.title}}</th>
                </tr>
            </thead>
            <!-- 表体 -->
            <tbody>
                <tr v-for="item in data" :key="item.id">
                    <td><input type="checkbox" :checked="isSingleChecked(item)" @change="(e) => selectedChange(item, e)"></td>
                    <td v-for="column in columns" :key="column.key">
                        {{item[column.key]}}
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
import CloneDeep from "lodash/cloneDeep";
export default {
    computed: {
        isAllChecked() {
            return this.selectedItems.length === this.data.length;
        }
    },
    watch: {
       selectedItems(newVal) {
            if (newVal.length !== this.data.length && newVal.length > 0) {
                this.$refs.allCheckbox.indeterminate = true
            } else {
                this.$refs.allCheckbox.indeterminate = false
            }
        }
    },
    data(){
        return {}
    },
    props: {
        selectedItems: {
            type: Array,
            default: () => []
        },
        columns: {
            type: Array,
            default: () => []
        },
        data: {
            type: Array,
            default: () => []
        },
        border: {
            type: Boolean,
            default: false
        },
        stripe: {
            type: Boolean,
            default: true
        }
    },
    methods: {
        selectedChange(item, e){
            let clonedSelectedItems = CloneDeep(this.selectedItems);
            if (e.target.checked) {
                clonedSelectedItems.push(item)
            } else {
                let idx = clonedSelectedItems.findIndex(n => n.id === item.id);
                clonedSelectedItems.splice(idx,1);
            }
            this.$emit('update:selectedItems', clonedSelectedItems); // .sync语法糖
        },
        selectedAllChange(e) {
            let clonedSelectedItems;
            if (e.target.checked) {
                clonedSelectedItems = CloneDeep(this.data)
            } else {
                clonedSelectedItems = []
            }
            this.$nextTick(() => {
                this.$emit('update:selectedItems', clonedSelectedItems);
            });
        },
        isSingleChecked(item) {
            return this.selectedItems.findIndex(n => n.id === item.id) > - 1
        }
    }
}
</script>
<style lang="stylus">
.table-wrapper {
    width: 80%;
    margin: 0 auto;
    table {
        border-spacing: 0;
        border-collapse: collapse;
        width: 100%;
        &.border {
            border: 1px solid #ccc;
            th,td {
                border: 1px solid #ccc;
            }
        }
        &.stripe {
            tbody {
                tr:nth-child(even) {
                    background: #eee;
                }
            }
        }
        th {
            background: #eee;
        }
        th, td {
            border-bottom: 1px solid #ccc;
            padding: 5px;
            text-align: left;
        }
    }
}
</style>