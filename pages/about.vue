<script setup lang="ts">
definePageMeta({
  documentDriven: false
})

const title = 'About - Kushagra Agrawal'
const description = 'Find out or about me as a person, my personal history, my business and open source contributions.'

useSeoMeta({
  title,
  description,
})

defineOgImageComponent('General')
</script>

<template>
  <div>
    <AppSection>
      <ParagraphDecoration />
      <AppParagraph look="heading" class="mt-4" tag="h1">About me</AppParagraph>
      <div class="lg:grid grid-cols-2 lg:items-end mt-16 lg:mt-0">
        <div class="lg:hidden">
          <img class="rounded-full mx-auto" width="192" height="192" src="/img/kush-pp.png"
            alt="Photo of Kushagra Agrawal">
        </div>
        <div class="-mt-16 lg:mt-0">
          <div class="prose lg:prose-lg lg:mt-8">
            <h2>Hey!</h2>
            <p>
            I am Kushagra Agrawal, a dedicated researcher with a keen interest in artificial intelligence and its applications. Currently pursuing my Bachelor of Technology at KIIT Deemed to be University, I have maintained a strong academic record, exploring deep learning models for Industry 4.0 and contributing to research in food safety and medical imaging. Serving as a reviewer for esteemed journals highlights my commitment to advancing knowledge in the scientific community.  
            </p>
            <p>
            As a student, I actively engage in extracurricular activities and societies like the IoT Lab and KIIT-Konnexions. Participation in conferences and seminars has broadened my skills in emerging technologies, complementing my academic achievements and certifications in IT support and language proficiency
            </p>
            <p>
            A builder at heart, I excel in translating ideas into impactful solutions. Leading projects like the SIH 2023 challenge on medicinal plant identification showcases my project management and problem-solving abilities. Projects integrating LLMs and Intel's Transformer extensions demonstrate my innovation in practical applications.
            </p>
            <p>
            Leadership and social responsibility drive my actions. From school leadership roles to volunteering in community outreach programs, I am committed to fostering positive change. Involvement in professional societies like IEEE allows me to promote technical skills and innovation among peers, furthering my dedication to societal welfare.
            </p>
            <h2>Skills</h2>

            <p>Various frameworks and libraries are a joy to work with! If I had to choose my dream tech stack though, I'd pick the following:</p>
            <p>For cloud platforms, I'm proficient in Google Cloud, AWS, and Microsoft Azure, enabling scalable and efficient deployment of applications. In programming, my expertise spans Java, Python, C, C++, Verilog, MATLAB, and LaTeX, providing a robust foundation for software development and academic research. I specialize in machine learning and artificial intelligence, leveraging TensorFlow and PyTorch for deep learning and supervised learning tasks. My skills extend to natural language processing, responsible AI practices, and computer vision applications, ensuring ethical and impactful AI solutions.</p>
            <p>With a solid grasp of development tools like Git, Docker, and Kubernetes, I streamline workflow processes and ensure seamless project management. Data processing and database management using Pandas, NumPy, Scikit-Learn, SQL, and Hadoop are integral to my analytical capabilities. I also have experience in web development with HTML, CSS, and JavaScript, enabling me to create interactive and user-friendly interfaces.</p>
            <p>Soft skills such as problem-solving, team collaboration, effective communication, leadership, and presentation skills complement my technical expertise, facilitating successful project execution and stakeholder engagement. With this versatile skill set, I aim to innovate and deliver impactful solutions in the ever-evolving tech landscape.</p>
            <AppButton to="https://drive.google.com/file/d/1QEgKlGB0nvWx3KZVkkibFPhVRcQiz-2m" look="secondary">Download <span class="hidden sm:inline">Resume</span></AppButton>
            <AppButton to="https://drive.google.com/file/d/1yXRK-dRtuV2UKoHfMlPycxIwQHiJ-fCQ" look="secondary">Download <span class="hidden sm:inline">Detailed CV</span></AppButton>

          </div>
        </div>
        <div class="hidden sticky bottom-0 lg:block">
          <NuxtPicture width="608" height="931" format="avif,webp,png" densities="x1 x2" placeholder
            :img-attrs="{ class: 'z-20 ml-24 -mb-24' }" src="/img/kush-about.png" alt=""
            aria-hidden />
        </div>
      </div>
    </AppSection>
  </div>
</template>
