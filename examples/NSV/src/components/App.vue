<script lang="ts">
  import { DateTimeFormat } from 'nativescript-intl'


  export default {
    data() {
      return {
        date: '2020-01-01',
        utcDate: '',
        currentTimeZoneDate: ''
      }
    },
    computed: {
      utcConfig(): any {
        return {
          year: 'numeric',
          month: 'short',
          day: 'numeric',
          timeZoneName: 'UTC',
        }
      },
      someConfig(): any {
        return {
          year: 'numeric',
          month: 'short',
          day: 'numeric',
        }
      },
    },
    methods: {
      getFormatter(config) : DateTimeFormat{
        return new DateTimeFormat("en", config)
      }
    },
    mounted(){
      const exampleDate =new Date(this.date);
      const utcFormatter : DateTimeFormat = this.getFormatter(this.utcConfig);
      this.utcDate = utcFormatter.format(exampleDate)

      const formatter : DateTimeFormat = this.getFormatter(this.someConfig);
      this.currentTimeZoneDate = formatter.format(exampleDate)
    }
  }
</script>

<template>
    <Page>
        <ActionBar title="Format Dates"/>
        <StackLayout>

            <Label class="message" text="Original date" col="0" row="0"/>
            <Label class="message" style="margin-bottom: 20" :text="date" col="0" row="0"/>
            
            <Label class="message" text="Formatted UTC date" col="0" row="0"/>
            <Label class="message" style="margin-bottom: 20" :text="utcDate" col="0" row="0"/>
            
            <Label class="message" text="Formatted date" col="0" row="0"/>
            <Label class="message" style="margin-bottom: 20" :text="currentTimeZoneDate" col="0" row="1"/>
        </StackLayout>
    </Page>
</template>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
