<template>
  <v-col cols="12" md="6" class="DataCard">
    <data-view
      :title="$t('検査実施状況')"
      :title-id="'details-of-tested-cases'"
      :date="Data.inspection_status_summary.date"
    >
      <template v-slot:description>
        <ul>
          <li>
            {{
              $t(
                '（注）検査実施人数には、医療機関等による検査人数、チャーター機帰国者、クルーズ船乗客等は含まれていない。'
              )
            }}
          </li>
          <li>
            {{
              $t(
                '（注）速報値として公開するものであり、後日確定データとして修正される場合あり'
              )
            }}
          </li>
        </ul>
      </template>
      <tested-cases-details-table
        :aria-label="$t('検査実施状況')"
        v-bind="testedCases"
      />
    </data-view>
  </v-col>
</template>

<script>
import Data from '@/data/data.json'
import formatTestedCases from '@/utils/formatTestedCases'
import DataView from '@/components/DataView.vue'
import TestedCasesDetailsTable from '@/components/TestedCasesDetailsTable.vue'

export default {
  components: {
    DataView,
    TestedCasesDetailsTable
  },
  data() {
    // 検査陽性者の状況
    const testedCases = formatTestedCases(Data.inspection_status_summary)

    return {
      Data,
      testedCases
    }
  }
}
</script>
