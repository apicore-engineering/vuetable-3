<script>
/* eslint-disable @typescript-eslint/camelcase */
import VuetableUI from "./VuetableCssTailwindUI.js";

export default {
  props: {
    css: {
      type: Object,
      default() {
        return {};
      }
    },
    infoTemplate: {
      type: String,
      default() {
        return "Displaying {from} to {to} of {total} items";
      }
    },
    noDataTemplate: {
      type: String,
      default() {
        return "No relevant data";
      }
    }
  },
  data: function () {
    return {
      tablePagination: null,
      customCss: {}
    };
  },
  computed: {
    paginationInfo() {
      if (this.tablePagination == null || this.tablePagination.total == 0) {
        return this.noDataTemplate;
      }

      return this.infoTemplate
                 .replace("{from}", this.tablePagination.from || 0)
                 .replace("{to}", this.tablePagination.to || 0)
                 .replace("{total}", this.tablePagination.total || 0);
    }
  },
  created() {
    this.mergeCss();
  },
  methods: {
    mergeCss() {
      this.customCss = {...VuetableUI.paginationInfo, ...this.css};
    },
    setPaginationData(tablePagination) {
      this.tablePagination = tablePagination;
    },
    resetData() {
      this.tablePagination = null;
    }
  }
};
</script>
