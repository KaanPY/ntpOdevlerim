using System.Data.SQLite; // SQLite kütüphanesini çağrıyoruz.

string programYolu = Application.StartupPath; // Programın çalştığı klasör yolu.

string sqliteYolu = $"Data source={programYolu}\\dbName.db;Version=3;";

using (var baglan = new SQLiteConnection(sqliteYolu)) // SQLite bağlantı.
{
	using(var komut = new SQLiteCommand($"SELECT * FROM kullanicilar WHERE id={textBox1.Text}", baglan))
	{
		try
		{
			komut.Connection.Open();
			SQLiteDataReader dtr = komut.ExecuteReader();
			if(dtr.Read())
			{
				textBox2.Text = dtr["kullaniciadi"].ToString();
				textBox3.Text = dtr["sifre"].ToString();
			}
		}
		catch (Exception hata)
		{
			MessageBox.Show(hata.Message);
		}
	}
}
