<template>
    <div>
        <kk-table 
            :columns="columns1" 
            :data="data1"
            border
            :selectedItems.sync = "selectedItems"
        />
    </div>
</template>
<script>
import kkTable from "./components/kk-table";
export default {
    components: {
        kkTable
    },
    data() {
        return {
            selectedItems: [],
            columns1: [
                {
                    title: 'Name',
                    key: 'name'
                },
                {
                    title: 'Age',
                    key: 'age'
                },
                {
                    title: 'Address',
                    key: 'address'
                }
            ],
            data1: [
                {
                    id: 1,
                    name: 'James Brown',
                    age: 18,
                    address: 'New York No.1 Lake Park',
                    data: '2016-10-03'
                },
                {
                    id: 2,
                    name: 'Kathy Green',
                    age: 28,
                    address: 'Sanfrancisco',
                    data: '2017-01-13'
                },
                {
                    id: 3,
                    name: 'Rachael Green',
                    age: 20,
                    address: 'LosAngeles',
                    data: '2014-11-23'
                },
                {
                    id: 4,
                    name: 'Johnson Castle',
                    age: 40,
                    address: 'England',
                    data: '2010-05-05'
                },
                {
                    id: 5,
                    name: 'Noah Trevor',
                    age: 30,
                    address: 'Johnhanasberg',
                    data: '2000-08-25'
                },
                {
                    id: 6,
                    name: 'Wang Jiaer',
                    age: 26,
                    address: 'Hong Kong',
                    data: '1994-08-04'
                },
                {
                    id: 7,
                    name: 'Wang Yibo',
                    age: 23,
                    address: 'Holland',
                    data: '1997-08-23'
                },
                {
                    id: 8,
                    name: 'Harry Porter',
                    age: 25,
                    address: 'Ireland',
                    data: '2008-06-10'
                }
            ]
        }
    }
}
</script>