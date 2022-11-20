# prjWebFriendBook
#Social Media website with .Net C#


using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data;         
using System.Data.OleDb;  

namespace prjWebCsFriendBook
{
    public partial class Login : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            
        }

        protected void btnConnexion_Click(object sender, EventArgs e)
        {
            string UserName = txtUserNameLog.Text.Trim();
            string passwordLog = txtPasswordLog.Text.Trim();

            

            OleDbConnection mycon = new OleDbConnection(@"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Users\Admin\source\repos\prjWebCsFriendBook\prjWebCsFriendBook\App_Data\PrjFriendBookDB.mdb;Persist Security Info=True" + Server.MapPath("~\\App_Data\\PrjFriendBookDB.mdb;Persist Security Info=True"));
            mycon.Open();

            // requete sql //
            string sql = "SELECT RefMembre FROM membres WHERE UserName = '" + UserName + "' AND MotPasse = '" + passwordLog + "'";

            OleDbCommand mycmd = new OleDbCommand(sql, mycon);
            OleDbDataReader myReader = mycmd.ExecuteReader();

            if (myReader.Read() == true) 
            {
                Session["MembreId"] = Convert.ToInt32(myReader["RefMembre"]);
                mycon.Close();
                Server.Transfer("acceuiil.aspx");
            }
            else
            {
                
                mycon.Close();
                lblErreurLog.Text = " Nom Utilisateur ou Mot de passe Invalid, Essayez encore ";
                
            }

            

        }

       
    }
}
