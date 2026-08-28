# NeuralEngineUltra Integration Guide

Follow these steps to successfully integrate the library into your Android project.

## Step 1: Add the JitPack Repository

Add the JitPack repository to your `settings.gradle.kts` file at the end of the `repositories` block:

```kotlin
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        mavenCentral()
        maven { url = uri("https://jitpack.io") }
    }
}
```

## Step 2: Configure Required Dependencies

Replace your existing `dependencies` block in your module-level `build.gradle.kts` with the following configuration to ensure all required underlying frameworks are present:

```kotlin
dependencies {
    // Compose
    implementation(platform(libs.androidx.compose.bom))
    implementation(libs.androidx.activity.compose)
    implementation(libs.androidx.compose.material3)
    implementation(libs.androidx.compose.ui)
    implementation(libs.androidx.compose.ui.graphics)
    implementation(libs.androidx.compose.ui.tooling.preview)
    implementation("androidx.compose.foundation:foundation")
    implementation("androidx.compose.material:material-icons-extended")

    // AndroidX Core & Lifecycle
    implementation(libs.androidx.core.ktx)
    implementation(libs.androidx.lifecycle.runtime.ktx)
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.9.1")
    implementation("androidx.lifecycle:lifecycle-runtime-compose:2.9.1")

    // Navigation
    implementation("androidx.navigation:navigation-compose:2.7.7")

    // ViewModel
    implementation(libs.androidx.lifecycle.viewmodel.ktx)

    // SQLCipher / SQLite
    api("net.zetetic:sqlcipher-android:4.17.0")
    api("androidx.sqlite:sqlite:2.6.2")

    // OkHttp
    implementation("com.squareup.okhttp3:okhttp:4.11.0")
    implementation("com.squareup.okhttp3:logging-interceptor:4.12.0")

    // Animation / Lottie
    implementation("com.airbnb.android:lottie-compose:6.4.0")

    // Constraint Layout
    implementation(libs.androidx.constraintlayout.compose)

    // Coil
    implementation(libs.coil.compose)

    // Google Sign-In
    implementation("com.google.android.gms:play-services-auth:21.5.0")

    // Media3
    implementation("androidx.media3:media3-exoplayer:1.8.0")
    implementation("androidx.media3:media3-ui:1.8.0")
    implementation("androidx.media3:media3-common:1.8.0")
    implementation("androidx.media3:media3-transformer:1.8.0")

    // AWS S3
    implementation("com.amazonaws:aws-android-sdk-core:2.46.0")
    implementation("com.amazonaws:aws-android-sdk-s3:2.46.0")

    // Local AAR
    implementation(files("libs/production-library-release.aar"))

    // Unit Tests
    testImplementation(libs.junit)

    // Android Tests
    androidTestImplementation(platform(libs.androidx.compose.bom))
    androidTestImplementation(libs.androidx.compose.ui.test.junit4)
    androidTestImplementation(libs.androidx.espresso.core)
    androidTestImplementation(libs.androidx.junit)

    // Debug
    debugImplementation(libs.androidx.compose.ui.test.manifest)
    debugImplementation(libs.androidx.compose.ui.tooling)

    //Then add your needed dependency
}
```

## Step 3: Add the Library Dependency

Add the specific library dependency to the same `dependencies` block:

```kotlin
dependencies {
    // Add this along with the dependencies from Step 2
    implementation("com.github.skynetbee:NeuralEngineUltra:2.0.1")
}
```

## Step 4: Initialize the Library

In your `MainActivity.kt`, add the following initialization sequence directly **above** your `setContent` block:

```kotlin
Packagename.init(packageName)
DevOps.init(this)
DF.init(this)

// 1. FIRST: Initialize the database connection
SQLize.initialize(this)

// 2. SECOND: Pass your schema so the tables are created
FrameWork.init(
    baseUrl = "https://www.skynetbee.org/skynetbee/",
    onSuccessRoute = "home_screen",
    databaseSchema = myDatabaseSchema,
)

// 3. THIRD: Initialize Neural Memory AFTER the tables are defined!
NM.init(this)
```

## Step 5: Define Schema and Set Content

Define your database schema above your UI logic, and initialize your navigation inside the `setContent` block:

```kotlin
val myDatabaseSchema = listOf(
    // 1. all_members_registered_details
    "all_members_registered_details" to listOf(
        "unique_member_id",
        "member_type",
        "work_type",
        "identity_number",
        "official_name",
        "board",
        "cls",
        "sec",
        "pet_name",
        "official_photo",
        "scanned_image_of_sign",
        "id_proof_front_side_photo",
        "id_proof_back_side_photo",
        "second_idproof_front_side_photo",
        "second_idproof_back_side_photo",
        "ghibli_photo",
        "date_of_birth",
        "time_of_birth",
        "sex",
        "phno_1",
        "phno_2",
        "mail_1",
        "mail_2",
        "address",
        "local_area",
        "aadhar_number",
        "pan_number",
        "qualification",
        "designation",
        "father_name",
        "father_business_or_work",
        "father_occupation_category",
        "father_designation",
        "father_occupation_in_detail",
        "father_annual_income",
        "father_occupation_address",
        "father_phno_1",
        "father_phno_2",
        "father_status",
        "mother_name",
        "mother_business_or_work",
        "mother_occupation_category",
        "mother_designation",
        "mother_occupation_in_detail",
        "mother_annual_income",
        "mother_occupation_address",
        "mother_phno_1",
        "mother_phno_2",
        "mother_status",
        "spouse_name",
        "spouse_business_or_work",
        "spouse_occupation_category",
        "spouse_designation",
        "spouse_occupation_in_detail",
        "spouse_annual_income",
        "spouse_occupation_address",
        "spouse_phno_1",
        "spouse_phno_2",
        "spouse_status",
        "no_of_siblings_or_children",
        "guardian1_name",
        "guardian1_relation",
        "guardian1_phno",
        "guardian2_name",
        "guardian2_relation",
        "guardian2_phno",
        "mother_tongue",
        "nationality",
        "native_place",
        "caste",
        "subcaste",
        "community",
        "religion",
        "blood_group",
        "if_relieved_date_of_quit"
    )
)

setContent {
    Background3()
    val myNavController = rememberNavController()
    Navigation(showGoogleSignIn = true) {
        composable("home_screen") {
            SyncTestScreen()
        }
    }
}
```

---

Created by Android Team, SkynetBee AI Pvt Ltd
