using System;
using System.Windows.Forms;

namespace LoginForm
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

            // Ẩn mật khẩu khi mở Form
            txtPassword.UseSystemPasswordChar = true;

            // Nhấn Enter -> Login
            this.AcceptButton = btnLogin;

            // Nhấn Esc -> Exit
            this.CancelButton = btnExit;

            // Gắn sự kiện
            chkShowPassword.CheckedChanged += chkShowPassword_CheckedChanged;
            btnLogin.Click += btnLogin_Click;
            btnExit.Click += btnExit_Click;
        }

        // Hiện / ẩn mật khẩu
        private void chkShowPassword_CheckedChanged(object sender, EventArgs e)
        {
            if (chkShowPassword.Checked)
            {
                // Tick -> hiện mật khẩu
                txtPassword.UseSystemPasswordChar = false;
            }
            else
            {
                // Bỏ tick -> ẩn mật khẩu
                txtPassword.UseSystemPasswordChar = true;
            }
        }

        // Nút Login
        private void btnLogin_Click(object sender, EventArgs e)
        {
            // Xóa thông báo lỗi cũ
            errorProvider.Clear();

            bool isValid = true;

            // Kiểm tra tên đăng nhập
            if (string.IsNullOrWhiteSpace(txtUsername.Text))
            {
                errorProvider.SetError(
                    txtUsername,
                    "Vui lòng nhập tên đăng nhập!"
                );

                isValid = false;
            }

            // Kiểm tra mật khẩu
            if (string.IsNullOrWhiteSpace(txtPassword.Text))
            {
                errorProvider.SetError(
                    txtPassword,
                    "Vui lòng nhập mật khẩu!"
                );

                isValid = false;
            }

            // Nếu có lỗi thì dừng
            if (!isValid)
            {
                return;
            }

            // Đăng nhập thành công
            MessageBox.Show(
                "Đăng nhập thành công!",
                "Thông báo",
                MessageBoxButtons.OK,
                MessageBoxIcon.Information
            );
        }

        // Nút Exit
        private void btnExit_Click(object sender, EventArgs e)
        {
            DialogResult result = MessageBox.Show(
                "Bạn có muốn thoát chương trình không?",
                "Xác nhận",
                MessageBoxButtons.YesNo,
                MessageBoxIcon.Question
            );

            if (result == DialogResult.Yes)
            {
                Application.Exit();
            }
        }
    }
}
