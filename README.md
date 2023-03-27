# ghalam78m
// Personal Health Tracker Page

        int score = PersonalHealthQuiz.score;
        bool quizfinished = PersonalHealthQuiz.quizfinished;

        public PersonalHealthPage()
        {
            InitializeComponent();

            if (quizfinished)
            {
                if (score < 9)
                {
                    health_condition.Text = "Not healthy -";
                    health_statement.Text = "You usually have health issues, which affect your other things in life and can cause much serious loss in future if continued like this. So, you must work towards improving your metabolism and immunity. Eat healthily, meditate and exercise.";
                    bad_face.Visibility = Visibility.Visible;

                    user_score.Content = score;
                }

                if (score >= 9 && score < 15)
                {
                    health_condition.Text = "Slightly Healthy -";
                    health_statement.Text = "Well, you are just normal healthy. It means that you are usually healthy but catch minor health issues from time to time. So, have some exercise, do some Yoga, have a healthy eating routine and see the changes.";
                    neutral_face.Visibility = Visibility.Visible;

                    user_score.Content = score;
                }

                if (score >= 15)
                {
                    health_condition.Text = "Healthy -";
                    health_statement.Text = "It's a sure thing that you are quite a healthy person, all credit to your determination, discipline and healthy eating. Keep it going on like this, you can enjoy many things in life only when you are healthy. So, what are you waiting for? Go, hit the gym if haven't already.";
                    good_face.Visibility = Visibility.Visible;

                    user_score.Content = score;
                }
            }
        }

        private void takequizBtn_Click(object sender, RoutedEventArgs e)
        {
            PersonalHealthQuiz.score = 0;
            PersonalHealthQuiz.quizfinished = false;

            PersonalHealthQuiz HealthQuiz = new PersonalHealthQuiz();
            this.Hide();
            HealthQuiz.Show();
        }
        
  --------------------------------------------------------------------------------------------------------------------------------------------------      
        
 // PersonalHealthQuiz

        // very healthy = 18
        // medium = 9
        // bad = 0

        public static int score = 0;
        public int questionsdone = 0;
        public static bool quizfinished = false;

        public PersonalHealthQuiz()
        {
            InitializeComponent();
        }

        private void question_A_Click(object sender, RoutedEventArgs e)
        {
            score += 3;
            questionsdone+= 1;

            if (questionsdone == 1)
            {
                question.Text = "Q2:  Do you avoid fried foods, dressing, cream sauces, gravy, butter, and margarine?";
                question_A.Content = "Yes, I always do!";
                question_B.Content = "I usually consume these things in moderation.";
                question_C.Content = "No, I eat them a lot.";

                user_score.Content = score;
            }

            if (questionsdone == 2)
            {
                question.Text = "Q3: Do you exercise at least 30 minutes on 3-5 days a week?";
                question_A.Content = "I exercise for almost an hour everyday.";
                question_B.Content = "I only exercise sometimes when I'm in the mood.";
                question_C.Content = "No I don't exercise.";

                user_score.Content = score;
            }

            if (questionsdone == 3)
            {
                question.Text = "Q4: Do you drink soda and eat typical snack foods (like chips, cookies, candy, etc) throughout the day and after dinner?";
                question_A.Content = "No, never.";
                question_B.Content = "Yeah, not regularly but sometimes.";
                question_C.Content = "Yeah mostly.";

                user_score.Content = score;
            }

            if (questionsdone == 4)
            {
                question.Text = "Q5: Do you drink at least 8 glasses of water a day?";
                question_A.Content = "Yes! I do.";
                question_B.Content = "I drink around that.";
                question_C.Content = "No, I barely drink water";

                user_score.Content = score;
            }

            if (questionsdone == 5)
            {
                question.Text = "Q6: Are you getting your recommended daily allowance of Calcium? Men = 1000mg Women under 50 = 1200mg Women over 50 = 1500mg";
                question_A.Content = "Yes! Definitely.";
                question_B.Content = "I have a regular intake of calcium";
                question_C.Content = "No, not at all";

                user_score.Content = score;
            }

            if (questionsdone == 6)
            {
                user_score.Content = score;
                quizfinished = true;

                PersonalHealthPage HealthPage = new PersonalHealthPage();
                MessageBox.Show("You have completed the quiz.");
                this.Hide();
                HealthPage.Show();
            }
        }

        private void question_B_Click(object sender, RoutedEventArgs e)
        {
            score += 1;
            questionsdone += 1;

            if (questionsdone == 1)
            {
                question.Text = "Q2:  Do you avoid fried foods, dressing, cream sauces, gravy, butter, and margarine?";
                question_A.Content = "Yes, I always do!";
                question_B.Content = "I usually consume these things in moderation.";
                question_C.Content = "No, I eat them a lot.";

                user_score.Content = score;
            }

            if (questionsdone == 2)
            {
                question.Text = "Q3: Do you exercise at least 30 minutes on 3-5 days a week?";
                question_A.Content = "I exercise for almost an hour everyday.";
                question_B.Content = "I only exercise sometimes when I'm in the mood.";
                question_C.Content = "No I don't exercise.";

                user_score.Content = score;
            }

            if (questionsdone == 3)
            {
                question.Text = "Q4: Do you drink soda and eat typical snack foods (like chips, cookies, candy, etc) throughout the day and after dinner?";
                question_A.Content = "No, never.";
                question_B.Content = "Yeah, not regularly but sometimes.";
                question_C.Content = "Yeah mostly.";

                user_score.Content = score;
            }

            if (questionsdone == 4)
            {
                question.Text = "Q5: Do you drink at least 8 glasses of water a day?";
                question_A.Content = "Yes! I do.";
                question_B.Content = "I drink around that.";
                question_C.Content = "No, I barely drink water";

                user_score.Content = score;
            }

            if (questionsdone == 5)
            {
                question.Text = "Q6: Are you getting your recommended daily allowance of Calcium? Men = 1000mg Women under 50 = 1200mg Women over 50 = 1500mg";
                question_A.Content = "Yes! Definitely.";
                question_B.Content = "I have a regular intake of calcium";
                question_C.Content = "No, not at all";

                user_score.Content = score;
            }

            if (questionsdone == 6)
            {
                user_score.Content = score;
                quizfinished = true;

                PersonalHealthPage HealthPage = new PersonalHealthPage();
                MessageBox.Show("You have completed the quiz.");
                this.Hide();
                HealthPage.Show();
            }
        }

        private void question_C_Click(object sender, RoutedEventArgs e)
        {
            questionsdone += 1;

            if (questionsdone == 1)
            {
                question.Text = "Q2:  Do you avoid fried foods, dressing, cream sauces, gravy, butter, and margarine?";
                question_A.Content = "Yes, I always do!";
                question_B.Content = "I usually consume these things in moderation.";
                question_C.Content = "No, I eat them a lot.";

                user_score.Content = score;
            }

            if (questionsdone == 2)
            {
                question.Text = "Q3: Do you exercise at least 30 minutes on 3-5 days a week?";
                question_A.Content = "I exercise for almost an hour everyday.";
                question_B.Content = "I only exercise sometimes when I'm in the mood.";
                question_C.Content = "No I don't exercise.";

                user_score.Content = score;
            }

            if (questionsdone == 3)
            {
                question.Text = "Q4: Do you drink soda and eat typical snack foods (like chips, cookies, candy, etc) throughout the day and after dinner?";
                question_A.Content = "No, never.";
                question_B.Content = "Yeah, not regularly but sometimes.";
                question_C.Content = "Yeah mostly.";

                user_score.Content = score;
            }

            if (questionsdone == 4)
            {
                question.Text = "Q5: Do you drink at least 8 glasses of water a day?";
                question_A.Content = "Yes! I do.";
                question_B.Content = "I drink around that.";
                question_C.Content = "No, I barely drink water";

                user_score.Content = score;
            }

            if (questionsdone == 5)
            {
                question.Text = "Q6: Are you getting your recommended daily allowance of Calcium? Men = 1000mg Women under 50 = 1200mg Women over 50 = 1500mg";
                question_A.Content = "Yes! Definitely.";
                question_B.Content = "I have a regular intake of calcium";
                question_C.Content = "No, not at all";

                user_score.Content = score;
            }

            if (questionsdone == 6)
            {
                user_score.Content = score;
                quizfinished = true;

                PersonalHealthPage HealthPage = new PersonalHealthPage();
                MessageBox.Show("You have completed the quiz.");
                this.Hide();
                HealthPage.Show();
            }
            
            // Happy sad neutral image source - https://www.canstockphoto.com/happy-neutral-and-sad-face-icons-87863610.html
        
        
