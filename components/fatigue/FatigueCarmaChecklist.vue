<template>
  <div>
    <ContentSection :caption="copy.caption" :title="copy.title" :content="copy.content">
      <p class="pb-6">
        Crew Resource Scheduling - 1-844-495-1049
      </p>
      <UAccordion :items="accordionItems" variant="outline" />
      <!--StackedList :questions="listSteps" /-->
    </ContentSection>
  </div>
</template>

<script lang="ts" setup>

const copy = {
  title: 'Calling in Fatigued',
  caption: 'CARMA Checklist',
  content: ['Any questions or concerns please email: FedEx-FRMC@alpa.org'],
};

const listSteps =
  [
    { text: 'Contact the company.', defaultOpen: true, caption: 'Crew Resource Scheduling', note: '1-844-495-1049', popoverText: '(paraphrasing CBA 12.A.9): A pilot who becomes excessively tired (fatigued) prior to or subsequent to trip shall notify CRS immediately and speak with the Duty Officer about their situation. If this happens during a trip and the decision is made to terminate the trip, the trip will end in that city. (Fatigue at domicile, during a hub turn (no legal rest between trips) is also treated as sick in the field.) 14.B.4-5' },
    { text: 'Arrange for rest', caption: 'Flight services desk', note: 'GT and hotel', popoverText: 'Work with the DO and Flight Services Desk (FSD) to arrange Ground Transportation and hotel for recovery.' },
    { text: 'Rest and recover.', popoverText: 'DO NOT make travel arrangements until you have RESTED and RECOVERED.' },
    { text: 'Make arrangements for return to base', caption: 'Deviate after coordination', popoverText: 'Fatigue in the field is treated like sick in the field (Section 14.B.4-5): “Company shall provide transportation, when the pilot is able to travel, back to his base”. If in the field, after rest, work with CRS, GT and Flight Services to deadhead back to Base. After required changes, and only then, can the crewmember deviate and make personal arrangements. (Pairing will only display activity up to fatigue call, nothing after).' },
    { text: 'After-Action', caption: 'File a fatigue report', note: 'File a DART', popoverText: 'An email sent to your company address will have a direct link. Secondary access is available via the PFC Report link where you will find your uncompleted report generated by the Duty Officer.' },
  ];

const accordionItems = listSteps.map(step => ({ label: step.text, defaultOpen: step.defaultOpen, content: step.popoverText }));

</script>
