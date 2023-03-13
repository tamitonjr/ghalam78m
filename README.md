# ghalam78m
#REGISTER
using MySql.Data.MySqlClient;
using System.Text.RegularExpressions;

namespace LoginAndRegister
{
    /// <summary>
    /// Interaction logic for Register.xaml
    /// </summary>
    public partial class Register : Window
    {
        bool loggedin = Login.loggedin;
        public Register()
        {
            InitializeComponent();
            if (loggedin)
            {
                MessageBox.Show("You need to be logged out to register an account.");
                this.Visibility = Visibility.Hidden;
                Home newHome = new Home();
                newHome.Show();
            }
            else
            {
                signoutBtn.Visibility = Visibility.Hidden;
            }
        }

        private void RegClick(object sender, RoutedEventArgs e)
        {
            string connStr = "server=ND-COMPSCI;" +
                             "user=S2100023_B_Adekunle;" +
                             "database=s2100023;" +
                             "port=3306;" +
                             "password=S2100023_B_Adekunle;";

            MySqlConnection conn = new MySqlConnection(connStr);

            try
            {
                conn.Open();
                string sql = "SELECT * FROM user_details";

                MySqlCommand cmd = new MySqlCommand(sql, conn);
                MySqlDataReader rdr = cmd.ExecuteReader();

                List<string> usernames = new List<string>();
                List<string> passwords = new List<string>();
                List<string> emails = new List<string>();

                while (rdr.Read())
                {
                    usernames.Add(rdr.GetString(1));
                    passwords.Add(rdr.GetString(2));
                    emails.Add(rdr.GetString(3));
                }

                rdr.Close();

                try
                {
                    bool validUser = ValidateUser();
                    bool validEmail = ValidateEmail();
                    bool validPass = ValidatePass();

                    if (validUser)
                    {
                        usertxt.Background = Brushes.Lime;
                    }
                    else
                    {
                        usertxt.Focus();
                        usertxt.Background = Brushes.Red;
                        MessageBox.Show("Your username must be at least 6 characters");
                    }

                    if (validEmail)
                    {
                        emailtxt.Background = Brushes.Lime;
                    }
                    else
                    {
                        emailtxt.Focus();
                        emailtxt.Background = Brushes.Red;
                        MessageBox.Show("Your Email Address is invalid");
                    }
                    if (validPass)
                    {
                        passtxt.Background = Brushes.Lime;
                    }
                    else
                    {
                        passtxt.Clear();
                        passtxt.Focus();
                        passtxt.Background = Brushes.Red;
                        MessageBox.Show("Password must be 6-12 AND include an uppercase letter");
                    }

                    if (validEmail && validPass && validUser)
                    {
                        try
                        {
                            string myUsername = usertxt.Text;
                            string myPassword = passtxt.Password.ToString();
                            string myEmail = emailtxt.Text;

                            string sqlcom = $"INSERT INTO user_details (username, password, email_address) VALUES ('{myUsername}', '{myPassword}', '{myEmail}')";

                            MySqlCommand sqlcmd = new MySqlCommand(sqlcom, conn);

                            sqlcmd.ExecuteNonQuery();

                            MessageBox.Show("Registration Successful");
                        }
                        catch (Exception)
                        {
                            MessageBox.Show("Registration Unsuccessful. Please try again");
                        }
                    }
                }
                catch (Exception ex)
                {
                    MessageBox.Show(ex.ToString());
                }
            }

            catch (Exception ex)
            {
                MessageBox.Show(ex.ToString());
            }
        }
        private bool ValidateEmail()
        {
            bool validEmail = false;

            validEmail = Regex.IsMatch(emailtxt.Text, @"^([\w\.\-]+)@([\w\-]+)((\.(\w){2,3})+)$");

            return validEmail;
        }

        private bool ValidatePass()
        {
            bool validPass = false;

            validPass = Regex.IsMatch(passtxt.Password.ToString(), @"^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{6,12}$");

            return validPass;
        }
        private bool ValidateUser()
        {
            bool validUser = false;

            validUser = Regex.IsMatch(usertxt.Text, @".{6}$");

            return validUser;
        }
        
        #LOGIN
using MySql.Data.MySqlClient;
using System.Text.RegularExpressions;

namespace LoginAndRegister
{
    /// <summary>
    /// Interaction logic for Login.xaml
    /// </summary>
    ///
    public partial class Login : Window
    {

        public static int id;
        public static bool loggedin;

        public Login()
        {
            InitializeComponent();
            signoutBtn.Visibility = Visibility.Hidden;
        }

        bool userpasscorrect = false;

        public void LoginClick(object sender, RoutedEventArgs e)
        {
            string connStr = "server=ND-COMPSCI;" +
                             "user=S2100023_B_Adekunle;" +
                             "database=s2100023;" +
                             "port=3306;" +
                             "password=S2100023_B_Adekunle;";

            MySqlConnection conn = new MySqlConnection(connStr);
            try
            {
                if (usertxt.Text == "" || passtxt.Password.ToString() == "")
                {
                    MessageBox.Show("One of the fields are blank.");
                }
                else
                {
                    try
                    {
                        conn.Open();

                        string sql = "SELECT * FROM user_details";

                        MySqlCommand cmd = new MySqlCommand(sql, conn);
                        MySqlDataReader rdr = cmd.ExecuteReader();

                        List<string> usernames = new List<string>();
                        List<string> passwords = new List<string>();

                        while (rdr.Read())
                        {
                            usernames.Add(rdr.GetString(1));
                            passwords.Add(rdr.GetString(2));
                        }

                        string myUsername = usertxt.Text;
                        string myPassword = passtxt.Password.ToString();

                        conn.Close();

                        for (int i = 0; i < usernames.Count; i++)
                        {
                            if (myUsername == usernames[i])
                            {
                                if (myPassword == passwords[i])
                                {
                                    userpasscorrect = true;
                                }
                                else
                                {
                                    MessageBox.Show("Login Unsuccesful, Please try again.");
                                }
                            }
                        }

                        if (userpasscorrect)
                        {
                            conn.Open();
                            loggedin = false;
                            string sql2 = $"SELECT user_details.userID FROM user_details WHERE username = '{myUsername}'";
                            MySqlCommand cmd2 = new MySqlCommand(sql2, conn);
                            MySqlDataReader rdr2 = cmd2.ExecuteReader();

                            List<int> userIDs = new List<int>();

                            while (rdr2.Read())
                            {
                                id = rdr2.GetInt32(0);
                            }

                            MessageBox.Show(id.ToString());

                            this.Visibility = Visibility.Hidden;
                            MessageBox.Show("Login Successful");
                            loggedin = true;
                            LoginBtn.Visibility = Visibility.Hidden;
                            Home newHome = new Home();
                            newHome.Show();
                        }
                    }
                    catch (Exception ex)
                    {
                        MessageBox.Show(ex.ToString());
                    }
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.ToString());
                //MessageBox.Show("Login Unsuccessful. Please try again");
            }

        }
