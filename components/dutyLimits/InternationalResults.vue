<template>
  <CardGrid>
    <CardGridItems :duty-limit-cards="dutyLimitCards" />
  </CardGrid>
</template>

<script lang="ts" setup>
import { minutesToHours, differenceInMinutes } from 'date-fns';
import { formatInTimeZone } from 'date-fns-tz';
import type { InternationalDuty } from '~/sched-committee-types';

const props = defineProps({
  internationalDutyLimits: {
    type: Object as PropType<InternationalDuty[]>,
    required: true,
  },

});

const dutyLimitCards = computed(() => {
  const internationalScheduledCards = props.internationalDutyLimits.map(dutyLimit =>
    ({
      title: 'Scheduled duty limit',
      notes: dutyLimit.scheduledNotes,
      duration: minutesToHours(dutyLimit.scheduled).toString(),
      minutes: dutyLimit.scheduled,
      dutyEndTime: formatInTimeZone(dutyLimit.endOfScheduledDutyDate, 'UTC', 'dd-MM HH:MM'),
      dutyEndTimeZulu: dutyLimit.endOfScheduledDutyDate,
      minutesRemaining: differenceInMinutes(dutyLimit.endOfScheduledDutyDate, new Date()),
      blockHours: dutyLimit.blockHours.scheduled ? `Block hours: ${dutyLimit.blockHours.scheduled}` : undefined,
      landings: dutyLimit.landings ? `Landings: ${dutyLimit.landings}` : undefined,
    }));

  const internationalOperationalCards = props.internationalDutyLimits.filter(dutyLimit => dutyLimit.operational !== undefined && dutyLimit.endOfOperationalDutyDate !== undefined).map(dutyLimit =>
    ({
      title: 'Operational duty limit',
      notes: dutyLimit.operationalNotes,
      duration: minutesToHours(dutyLimit.operational!).toString(),
      minutes: dutyLimit.operational!,
      dutyEndTime: dutyLimit.endOfOperationalDutyDate! && formatInTimeZone(dutyLimit.endOfOperationalDutyDate!, 'UTC', 'dd-MM HH:MM'),
      dutyEndTimeZulu: dutyLimit.endOfOperationalDutyDate!,
      minutesRemaining: dutyLimit.endOfOperationalDutyDate! && differenceInMinutes(dutyLimit.endOfOperationalDutyDate!, new Date()),
      blockHours: typeof dutyLimit?.blockHours.operational === 'number' ? `${dutyLimit?.blockHours.operational} block hours` : typeof dutyLimit?.blockHours.operational === 'string' ? dutyLimit?.blockHours.operational : undefined,
      landings: dutyLimit.landings ? `Landings: ${dutyLimit.landings}` : undefined,
    }));

  return [...internationalScheduledCards, ...internationalOperationalCards];
},
);

</script>

<style>

</style>
