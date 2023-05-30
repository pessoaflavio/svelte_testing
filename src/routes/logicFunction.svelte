<script context='module'>

    export function reduceCategories(listPicks){
        let store = []
        let dictval = {}
        console.log('hey')
        console.log(listPicks)
        listPicks.forEach(item => {
            let medium = item.medium
            if (store.includes(medium)==false){
                store.push(medium);
                dictval[medium] = 1
            } else {
                dictval[medium] += 1
            }
        }
        )
        console.log(store)
        console.log(dictval)
        let uniques = new Set(store)
        let uniqueArray = [...uniques]
        return {'arr': uniqueArray, 'val':dictval}
    }

</script>