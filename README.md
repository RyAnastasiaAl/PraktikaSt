namespace Столовая
{
    public partial class authorization : Form
    {
        public authorization()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            using (var db = new СтоловаяEntities())
            {
                var res = db.Пользователь.FirstOrDefault(item => item.Логин == loginBox.Text && item.Пароль == passwordBox.Text);
                if (res != null)
                {
                    var d = db.Пользователь.FirstOrDefault(item => item.Логин == loginBox.Text);


                    if (res.Роль == "Заведующий")
                    {
                        MessageBox.Show("Вы вошли под учетной записью, " + res.Роль);
                        Form zav = new FormZav();
                        zav.Show();
                        this.Hide();
                    }
                   

                    if (res.Роль == "Администратор")
                    {
                        MessageBox.Show("Вы вошли под учетной записью, " + res.Роль);
                        Form addpr = new FormAddPr();
                        addpr.Show();
                        this.Hide();
                    }
                    else
                    {
                        var s = db.Пользователь.FirstOrDefault(item => item.Логин == loginBox.Text);
                        MessageBox.Show("Неверный логин или пароль");
                    }

                }



            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            Form reg = new registrazia();
            reg.FormClosing += authorization_FormClosing;
            reg.Show();
            this.Hide();
        }

        private void authorization_FormClosing(object sender, FormClosingEventArgs e)
        {
            Application.Exit();
        }
    }
}
