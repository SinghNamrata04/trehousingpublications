<template>
    <h2 class="text-center"><u class="underline">JobOpportunities</u></h2>
    <div class="overflow-hidden px-4">

    <div class="relative w-full">
      <!-- Left Arrow Button (Hidden on Mobile) -->
      
      <!-- <button @click="scrollLeft" class="left-click hidden md:flex" style="color: aliceblue; background-color: aquamarine;"> </button>
       -->
       <button @click="scrollLeft" class="bottom"><span>&#10216;</span></button>


      <!-- Job Cards Wrapper -->
      <div 
        class="job-cards-container flex gap-4 overflow-x-auto md:overflow-hidden" 
        ref="jobCardsWrapper"
        @touchstart="startTouch"
        @touchmove="moveTouch"
      >
        <div v-for="(job, index) in visibleJobs" :key="index" class="job-card">
          <h3 class="text-lg font-bold">{{ job.title }}</h3>
          
          <div class="job-details">
            <p class="text-gray-600 flex items-center"><span>📍</span>{{ job.location }}</p>
            <p class="date-text flex items-center"><span>📅</span>{{ job.date }}</p>
            <p class="salary-text flex items-center"><span>💰</span>{{ job.salary }}</p>
          </div>

          <!-- Clickable Button for Previous Year Papers -->
          <button 
            @click="viewPreviousYearPaper(job)" 
            class="button-text"
          >
            👁 View Previous Year Paper
          </button>
        </div>
      </div>
      <button @click="scrollRight" class="button"><span>&#10217;</span></button>

      <!-- Right Arrow Button (Hidden on Mobile) -->
      <!-- <button @click="scrollRight" class="right-click" hidden md:flex></button> -->

    </div>
  </div>
</template>

<script>
export default {
    name: 'JobOpportunities',
    
  data() {
    return {
      jobs: [
        { title: "Government Clerk SHO", location: "Gujarat Government", date: "03-03-2025", salary: "40k to 50k" },
        { title: "BPSC Assistance Vacancy", location: "Patna, Bihar", date: "03-03-2025", salary: "50k to 60k" },
        { title: "Bihar Police Services", location: "Patna, Bihar", date: "03-03-2025", salary: "40k to 50k" },
        { title: "Railway Engineer", location: "New Delhi", date: "03-03-2025", salary: "60k to 80k" },
        { title: "UPSC Civil Services", location: "India", date: "03-03-2025", salary: "70k to 90k" },
        { title: "Paper 6", location: "India", date: "03-03-2025", salary: "70k to 90k" },
      ],
      currentIndex: 0,
      startX: 0,
    };
  },
  computed: {
    visibleJobs() {
      return this.jobs.slice(this.currentIndex, this.currentIndex + 3);
    }
  },
  
  methods: {
    scrollLeft() {
      if (this.currentIndex > 0) {
        this.currentIndex--;
      }
    },
    scrollRight() {
      if (this.currentIndex < this.jobs.length - 3) {
        this.currentIndex++;
      }
    },
    viewPreviousYearPaper(job) {
  const formattedTitle = job.title.replace(/\s+/g, '-').toLowerCase();
  const url = `https://example.com/previous-year-paper/${formattedTitle}`; // Enclose the URL in backticks (` `) for template literals
  window.open(url, '_blank');
},



    startTouch(e) {
      this.startX = e.touches[0].clientX;
      this.scrollLeft = this.$refs.jobCardsWrapper.scrollLeft;
    },
    moveTouch(e) {
      const touchMoveX = e.touches[0].clientX;
      const moveDistance = this.startX - touchMoveX;
      this.$refs.jobCardsWrapper.scrollLeft = this.scrollLeft + moveDistance;
    }
  }
};
</script>

<style scoped>
.overflow-hidden {
  background-color:#052A63;
}
.text-center{
  color: #0152CC;
  font-size: medium;
  padding: 10px;
  background-color: #fff;
}
.underline{
  color: #0152CC;
}

.button {
  position: absolute;
  top: 310%;
  right:-9px; /* Move it to the right side */
  transform: translateY(-50%);
  padding: 8px 12px;
  font-size: 40px;
  border: none;
  background-color: #052A63;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  width:221px;
  color: gray;
}

/* Move button after the third job card */
.job-card:nth-child(3) ~ .button {
  position: absolute;
  right: -40px; /* Position after the third card */
}


.bottom{
    padding: 8px 12px;  /* Smaller padding */
  font-size: 40px;  /* Reduced font size */
  border: none;  /* Removes default button border */
  background-color: #052A63;  /* Makes the button background transparent */
  cursor: pointer;  /* Adds pointer cursor on hover */
  align-items: start;
  justify-content: space-around;
  position: absolute;
  display: flex;
  top:1950px;
  width:200px;
  transform: translateY(-50%);
  color: gray;
}

.button-text {
  background-color: #0152CC;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  width: 100%;
  padding: 8px 0; /* Adjusted padding */
  margin-top: auto; /* Pushes button to the bottom */
  font-size: 0.9rem;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s ease-in-out;
  text-align: center; /* Ensures it's centered */
}


.job-card .button-text {
  margin-top: auto; /* Ensures button is at the bottom */
}

.button-text:hover {
  background-color: darkblue;
}

/* Container for the job cards */
.job-cards-container {
  display: flex;
  gap: 10px; 
  overflow-x: auto;
  scroll-behavior: smooth;
  padding: 8px; 
  justify-content: center;
  margin: 0 auto;
  max-width: fit-content;
  margin-top: 50px;
  margin-bottom: 50px;
}

/* Buttons for navigation */

/* .left-click{
  padding: 10px;
  border-radius: 50%;
  cursor: pointer;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
}
.right-click{
  padding: 10px;
  border-radius: 50%;
  cursor: pointer;
  border: none;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
} */




/* Job Card Styles */
.job-card {
  width: 290px; /* Increased width */
  height: 250px; /* Keep the height as is or adjust if necessary */
  background: white;
  padding: 8px;
  border-radius: 0;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: left;
  overflow: hidden;
  position: relative;
}


.job-card .job-details {
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Space the paragraphs evenly */
  text-align: left;
  margin-top: 5px;
}

.job-card .job-details p {
  margin: 8px 0; /* Adds space between each <p> tag */
  flex-grow: 1; /* Ensures equal space distribution */
}
.date-text, .salary-text {
  margin: 0; /* Remove margin if necessary */
}

.date-text{
  text-align: left;
  margin: 4px 0;
  color: orange;
}
.salary-text {
  color: blue;
  text-align: left;
  margin: 4px 0;
}
.job-card h3 {
  font-size: 1.1rem; /* Decrease the font size */
  font-weight: bold; /* Make the text bold */
}


.job-card::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg, #463CD7 0%, #FF1702 100%);
}

/* Responsive Design */
@media (max-width: 768px) {
  .job-card {
    width: 200px;
    height: 230px; /* Adjusted height */
  }

  .job-cards-container {
    flex-wrap: nowrap;
    overflow-x: scroll;
    scroll-snap-type: x mandatory;
  }

  .job-card {
    scroll-snap-align: start;
  }
}
</style>