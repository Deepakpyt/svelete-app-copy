<script lang="ts">
  import Timeline from "$lib/components/Timeline.svelte";
  import TimelineItem from "$lib/components/TimelineItem.svelte";
  import TimelineSeparator from "$lib/components/TimelineSeparator.svelte";
  import TimelineDot from "$lib/components/TimelineDot.svelte";
  import TimelineConnector from "$lib/components/TimelineConnector.svelte";
  import TimelineContent from "$lib/components/TimelineContent.svelte";
  import TimelineOppositeContent from "$lib/components/TimelineOppositeContent.svelte";

  let showSummary = true;
  let showTimeline = false;

  function handleSummary() {
    showSummary = true;
    showTimeline = false;
  }
  function handleTimeline() {
    showSummary = false;
    showTimeline = true;
  }

  const colors = {
    first: "#7CD5E2",
    second: "#FEC048",
    third: "#DD84C1",
    forth: "#FB6958",
  };

  const items = [
    { year: "Nov 21", title: "Joined Nashtech", color: colors.first },
    { year: "Jan 22", title: "Completed KIP", color: colors.second },
    { year: "July 22", title: "Completed KUP", color: colors.third },
    { year: "July 22", title: "Job Title Changed", color: colors.forth },
  ];

  export let showModal = false;
  export let viewData: any = {
    employee_name: "John Doe",
    employee_id: "12345",
    employee_batch: "Batch 2023",
    employee_email: "john.doe@example.com",
    employee_status: "Active",
    practice: "Software Development",
    employee_details: {
      personal_email: "johndoe@gmail.com",
      age: 30,
      dob: "1994-05-01",
      gender: "Male",
      phone_number: "123-456-7890",
      github_id: "johnDoeGitHub",
      address: "123 Main St, City, Country",
      education: {
        degree: "Bachelor of Science in Computer Science",
        college_name: "XYZ University",
        completion_year: "2016",
        percentage: "85%",
      },
    },
  };

  function handleClose(event: any) {
    event.preventDefault();
    showModal = false;
  }
</script>

{#if showModal}
  <div class="modal-container flex flex-col">
    <div class="modal-background" on:click={handleClose} />
    <div class="modal-content">
      <div class="prose">
        <h2 class="text-4xl font-bold text-center mb-10">Employee Details</h2>
        <div class="switches-container">
          <input
            type="radio"
            class:selected={showSummary}
            on:click={handleSummary}
            id="Summary"
            name="switchTimelines"
            value="Summary"
            checked="checked"
          />
          <input
            type="radio"
            class:selected={showTimeline}
            on:click={handleTimeline}
            id="Timeline"
            name="switchTimelines"
            value="Timeline"
          />
          <label for="Summary">Summary</label>
          <label for="Timeline">Timeline</label>
          <div class="switch-wrapper">
            <div class="switch">
              <div>Summary</div>
              <div>Timeline</div>
            </div>
          </div>
        </div>
        {#if showSummary}
          <div class="grid-container">
            <div class="bg-aliceblue p-4 shadow-md">
              <h2 class="section-title">Basic Details</h2>
              <div class="info-item">
                <p class="label">Name:</p>
                <p class="value">{viewData.employee_name}</p>
              </div>
              <div class="info-item">
                <p class="label">Employee Id:</p>
                <p class="value">{viewData.employee_id}</p>
              </div>
              <div class="info-item">
                <p class="label">Batch:</p>
                <p class="value">{viewData.employee_batch}</p>
              </div>
              <div class="info-item">
                <p class="label">Email:</p>
                <p class="value">{viewData.employee_email}</p>
              </div>
              <div class="info-item">
                <p class="label">Status:</p>
                <p class="value">{viewData.employee_status}</p>
              </div>
              <div class="info-item">
                <p class="label">Practice:</p>
                <p class="value">{viewData.practice}</p>
              </div>
            </div>

            <div class="bg-aliceblue p-4 shadow-md">
              <h2 class="section-title">Personal Information</h2>
              <div class="info-item">
                <p class="label">Work Email:</p>
                <p class="value">{viewData.employee_email}</p>
              </div>
              <div class="info-item">
                <p class="label">Personal Email:</p>
                <p class="value">{viewData.employee_details.personal_email}</p>
              </div>
              <div class="info-item">
                <p class="label">Age:</p>
                <p class="value">{viewData.employee_details.age}</p>
              </div>
              <div class="info-item">
                <p class="label">Date of Birth:</p>
                <p class="value">{viewData.employee_details.dob}</p>
              </div>
              <div class="info-item">
                <p class="label">Gender:</p>
                <p class="value">{viewData.employee_details.gender}</p>
              </div>
              <div class="info-item">
                <p class="label">Phone Number:</p>
                <p class="value">{viewData.employee_details.phone_number}</p>
              </div>
              <div class="info-item">
                <p class="label">GitHub ID:</p>
                <p class="value">{viewData.employee_details.github_id}</p>
              </div>
              <div class="info-item">
                <p class="label">Address:</p>
                <p class="value">{viewData.employee_details.address}</p>
              </div>
            </div>

            <div class="bg-aliceblue p-4 shadow-md">
              <h2 class="section-title">Education Qualification</h2>
              <div class="info-item">
                <p class="label">Degree:</p>
                <p class="value">
                  {viewData.employee_details.education.degree}
                </p>
              </div>
              <div class="info-item">
                <p class="label">College Name:</p>
                <p class="value">
                  {viewData.employee_details.education.college_name}
                </p>
              </div>
              <div class="info-item">
                <p class="label">Date of Completion:</p>
                <p class="value">
                  {viewData.employee_details.education.completion_year}
                </p>
              </div>
              <div class="info-item">
                <p class="label">Percentage:</p>
                <p class="value">
                  {viewData.employee_details.education.percentage}
                </p>
              </div>
            </div>
          </div>
        {/if}

        {#if showTimeline}
          <div class="personal-info">
            <h2 class="section-title">Timeline</h2>
            <Timeline position="alternate">
              {#each items as item}
                <TimelineItem>
                  <TimelineOppositeContent slot="opposite-content">
                    <p class="oposite-content-title">{item.year}</p>
                  </TimelineOppositeContent>
                  <TimelineSeparator>
                    <TimelineDot style={`background-color: ${item.color};`} />
                    <TimelineConnector />
                  </TimelineSeparator>
                  <TimelineContent>
                    <h3 class="content-title">{item.title}</h3>
                  </TimelineContent>
                </TimelineItem>
              {/each}
            </Timeline>
          </div>
        {/if}
        <button class="dialog-close-button" on:click={handleClose}>Close</button
        >
      </div>
    </div>
  </div>
{/if}

<style>
  .modal-container {
    position: fixed;
    z-index: 1000;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .grid-container {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 3rem;
  }
  .modal-background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.8);
    z-index: 900;
  }
  .bg-aliceblue {
    background-color: aliceblue;
    border-radius: 10px;
    margin-top: 1rem;
  }
  .modal-content {
    overflow: auto;
    position: relative;
    z-index: 1000;
    background-color: #fff;
    padding: 20px;
    border-radius: 4px;
    text-align: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.16);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 25%;
    height: 95%;
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .tab {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-bottom: 1rem;
  }

  button.selected {
    background-color: #d60016;
    color: #fff;
  }

  button {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    background-color: #f5f5f5;
    color: #555;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #e0e0e0;
  }
  .prose {
    width: 100%;
  }
  .section-title {
    font-size: 1.25rem;
    font-weight: bold;
    margin-bottom: 0.25rem;
  }

  .info-item {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.25rem;
    font-size: 0.9rem;
  }

  .dialog-close-button {
    padding: 10px 20px;
    margin-top: 1rem;
    border: none;
    background-color: #d60016;
    color: #fff;
    cursor: pointer;
    border-radius: 4px;
  }

  .dialog-close-button:hover {
    background-color: #b40012;
  }
  @media (max-width: 700px) {
    .modal-content {
      width: 90%;
      left: 44%;
    }
    .prose {
      width: 102%;
    }
  }
  @media (max-width: 375px) {
    .modal-content {
      width: 90%;
      left: 44%;
    }
    .prose {
      width: 110%;
    }
  }
  @media (max-width: 425) {
    .modal-content {
      width: 90%;
      left: 44%;
    }
    .prose {
      width: 103%;
    }
  }
  @media (max-width: 768) {
    .modal-content {
      width: 90%;
      left: 44%;
    }
    .prose {
      width: 100%;
    }
  }

  .switches-container {
    width: 16rem;
    position: relative;
    display: flex;
    padding: 0;
    position: relative;
    background: var(--switches-bg-color);
    line-height: 3rem;
    border-radius: 7px;
    margin-left: auto;
    margin-right: auto;
    box-shadow: rgba(0, 0, 0, 0.02) 0px 1px 3px 0px,
      rgba(27, 31, 35, 0.15) 0px 0px 0px 1px;
  }

  /* input (radio) for toggling. hidden - use labels for clicking on */
  .switches-container input {
    visibility: hidden;
    position: absolute;
    top: 0;
  }

  /* labels for the input (radio) boxes - something to click on */
  .switches-container label {
    width: 50%;
    padding: 0;
    margin: 0;
    text-align: center;
    cursor: pointer;
    color: var(--switches-label-color);
  }

  /* switch highlighters wrapper (sliding left / right)
    - need wrapper to enable the even margins around the highlight box
*/
  .switch-wrapper {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 50%;
    z-index: 3;
    transition: transform 0.5s cubic-bezier(0.77, 0, 0.175, 1);
    /* transition: transform 1s; */
  }

  /* switch box highlighter */
  .switch {
    border-radius: 7px;
    background: var(--switch-bg-color);
    height: 100%;
  }

  /* switch box labels
    - default setup
    - toggle afterwards based on radio:checked status
*/
  .switch div {
    width: 100%;
    text-align: center;
    opacity: 0;
    display: block;
    color: var(--switch-text-color);
    transition: opacity 0.2s cubic-bezier(0.77, 0, 0.175, 1) 0.125s;
    will-change: opacity;
    position: absolute;
    top: 0;
    left: 0;
  }

  /* slide the switch box from right to left */
  .switches-container input:nth-of-type(1):checked ~ .switch-wrapper {
    transform: translateX(0%);
  }

  /* slide the switch box from left to right */
  .switches-container input:nth-of-type(2):checked ~ .switch-wrapper {
    transform: translateX(100%);
  }

  /* toggle the switch box labels - first checkbox:checked - show first switch div */
  .switches-container
    input:nth-of-type(1):checked
    ~ .switch-wrapper
    .switch
    div:nth-of-type(1) {
    opacity: 1;
  }

  /* toggle the switch box labels - second checkbox:checked - show second switch div */
  .switches-container
    input:nth-of-type(2):checked
    ~ .switch-wrapper
    .switch
    div:nth-of-type(2) {
    opacity: 1;
  }
</style>
