<template>
  <hot-table ref="hotTableComponent" :data="data" :settings="hotSettings"></hot-table>
</template>

<script lang="ts">
import { HotTable } from '@handsontable/vue';
import 'handsontable/dist/handsontable.full.css';

import { getData } from "../utils/constants";
import { progressBarRenderer } from "../renderers/progressBar";
import { starsRenderer } from "../renderers/stars";

import {
  alignHeaders,
  drawCheckboxInRowHeaders,
  addClassesToRows,
  changeCheckboxCell
} from "../utils/hooks-callbacks";

export default {
  name: 'DataGrid',
  data: function() {
    return {
      hotSettings: {
        height: 450,
        dropdownMenu: true,
        manualRowMove: true,
        hiddenColumns: {
          indicators: true,
        },
        contextMenu: true,
        multiColumnSorting: true,
        filters: true,
        rowHeaders: true,
        afterOnCellMouseDown: changeCheckboxCell,
        afterGetColHeader: alignHeaders,
        afterGetRowHeader: drawCheckboxInRowHeaders,
        beforeRenderer: addClassesToRows,
        colWidths: [140, 192, 100, 90, 90, 110, 97, 100, 126],
        colHeaders: [
          "Company name",
          "Name",
          "Sell date",
          "In stock",
          "Qty",
          "Progress",
          "Rating",
          "Order ID",
          "Country"
        ],
        columns: [
          { data: 1, type: "text" },
          { data: 3, type: "text" },
          {
            data: 4,
            type: "date",
            allowInvalid: false
          },
          {
            data: 6,
            type: "checkbox",
            className: "htCenter"
          },
          {
            data: 7,
            type: "numeric"
          },
          {
            data: 8,
            renderer: progressBarRenderer,
            readOnly: true,
            className: "htMiddle"
          },
          {
            data: 9,
            renderer: starsRenderer,
            readOnly: true,
            className: "star htCenter",
          },
          { data: 5, type: "text" },
          { data: 2, type: "text" }
        ],
        licenseKey: "non-commercial-and-evaluation",
      },
      data: getData()
    }
  },
  components: {
    HotTable
  }
}
</script>

<style lang="scss">
/*
  A stylesheet customizing app (custom renderers)
*/

table.htCore {
  tr.odd td {
    background: #fafbff;
  }

  tr.selected td {
    background: #edf3fd;
  }

  td .progressBar {
    background: #37bc6c;
    height: 10px;
  }

  td.star {
    color: #fcb515;
  }
}

/*
  A stylesheet customizing Handsontable style
*/

.handsontable {
  font-size: 13px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
  'Ubuntu', 'Helvetica Neue', Arial, sans-serif;
  font-weight: 400;

  .collapsibleIndicator {
    text-align: center;
  }
}
</style>
