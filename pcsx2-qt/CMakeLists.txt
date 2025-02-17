set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)

add_executable(pcsx2-qt)

if (PACKAGE_MODE)
	message(FATAL_ERROR "Package mode is not supported for Qt builds.")
else()
	install(TARGETS pcsx2-qt DESTINATION ${CMAKE_SOURCE_DIR}/bin)
endif()

target_sources(pcsx2-qt PRIVATE
	AboutDialog.cpp
	AboutDialog.h
	AboutDialog.ui
	AutoUpdaterDialog.cpp
	AutoUpdaterDialog.h
	AutoUpdaterDialog.ui
	CoverDownloadDialog.cpp
	CoverDownloadDialog.h
	CoverDownloadDialog.ui
	DisplayWidget.cpp
	DisplayWidget.h
	EarlyHardwareCheck.cpp
	MainWindow.cpp
	MainWindow.h
	MainWindow.ui
	PrecompiledHeader.cpp
	PrecompiledHeader.h
	QtHost.cpp
	QtHost.h
	QtKeyCodes.cpp
	QtProgressCallback.cpp
	QtProgressCallback.h
	QtUtils.cpp
	QtUtils.h
	SettingWidgetBinder.h
	GameList/EmptyGameListWidget.ui
	GameList/GameListModel.cpp
	GameList/GameListModel.h
	GameList/GameListRefreshThread.cpp
	GameList/GameListRefreshThread.h
	GameList/GameListWidget.cpp
	GameList/GameListWidget.h
	Settings/AdvancedSettingsWidget.cpp
	Settings/AdvancedSettingsWidget.h
	Settings/AdvancedSettingsWidget.ui
	Settings/AudioSettingsWidget.cpp
	Settings/AudioSettingsWidget.h
	Settings/AudioSettingsWidget.ui
	Settings/BIOSSettingsWidget.cpp
	Settings/BIOSSettingsWidget.h
	Settings/BIOSSettingsWidget.ui
	Settings/ControllerBindingWidget.ui
	Settings/ControllerBindingWidget_DualShock2.ui
	Settings/ControllerBindingWidgets.cpp
	Settings/ControllerBindingWidgets.h
	Settings/ControllerGlobalSettingsWidget.cpp
	Settings/ControllerGlobalSettingsWidget.h
	Settings/ControllerGlobalSettingsWidget.ui
	Settings/ControllerMacroEditWidget.ui
	Settings/ControllerMacroWidget.ui
	Settings/ControllerSettingsDialog.cpp
	Settings/ControllerSettingsDialog.h
	Settings/ControllerSettingsDialog.ui
	Settings/ControllerSettingWidgetBinder.h
	Settings/CreateMemoryCardDialog.cpp
	Settings/CreateMemoryCardDialog.h
	Settings/CreateMemoryCardDialog.ui
	Settings/EmulationSettingsWidget.cpp
	Settings/EmulationSettingsWidget.h
	Settings/EmulationSettingsWidget.ui
	Settings/FolderSettingsWidget.cpp
	Settings/FolderSettingsWidget.h
	Settings/FolderSettingsWidget.ui
	Settings/GameFixSettingsWidget.cpp
	Settings/GameFixSettingsWidget.h
	Settings/GameFixSettingsWidget.ui
	Settings/GameListSettingsWidget.cpp
	Settings/GameListSettingsWidget.h
	Settings/GameListSettingsWidget.ui
	Settings/GameSummaryWidget.cpp
	Settings/GameSummaryWidget.h
	Settings/GameSummaryWidget.ui
	Settings/GraphicsSettingsWidget.cpp
	Settings/GraphicsSettingsWidget.h
	Settings/GraphicsSettingsWidget.ui
	Settings/HotkeySettingsWidget.cpp
	Settings/HotkeySettingsWidget.h
	Settings/InputBindingDialog.cpp
	Settings/InputBindingDialog.h
	Settings/InputBindingDialog.ui
	Settings/InputBindingWidget.cpp
	Settings/InputBindingWidget.h
	Settings/InterfaceSettingsWidget.cpp
	Settings/InterfaceSettingsWidget.h
	Settings/InterfaceSettingsWidget.ui
	Settings/MemoryCardConvertDialog.cpp
	Settings/MemoryCardConvertDialog.h
	Settings/MemoryCardConvertDialog.ui
	Settings/MemoryCardConvertWorker.cpp
	Settings/MemoryCardConvertWorker.h
	Settings/MemoryCardSettingsWidget.cpp
	Settings/MemoryCardSettingsWidget.h
	Settings/MemoryCardSettingsWidget.ui
	Settings/DEV9DnsHostDialog.cpp
	Settings/DEV9DnsHostDialog.h
	Settings/DEV9DnsHostDialog.ui
	Settings/DEV9SettingsWidget.cpp
	Settings/DEV9SettingsWidget.h
	Settings/DEV9SettingsWidget.ui
	Settings/DEV9UiCommon.cpp
	Settings/DEV9UiCommon.h
	Settings/HddCreateQt.cpp
	Settings/HddCreateQt.h
	Settings/SettingsDialog.cpp
	Settings/SettingsDialog.h
	Settings/SettingsDialog.ui
	Tools/InputRecording/NewInputRecordingDlg.cpp
	Tools/InputRecording/NewInputRecordingDlg.h
	Tools/InputRecording/NewInputRecordingDlg.ui
	resources/resources.qrc
)

if(USE_ACHIEVEMENTS)
	target_sources(pcsx2-qt PRIVATE
		Settings/AchievementLoginDialog.cpp
		Settings/AchievementLoginDialog.h
		Settings/AchievementLoginDialog.ui
		Settings/AchievementSettingsWidget.cpp
		Settings/AchievementSettingsWidget.h
		Settings/AchievementSettingsWidget.ui
	)
endif()

target_precompile_headers(pcsx2-qt PRIVATE PrecompiledHeader.h)

target_include_directories(pcsx2-qt PRIVATE
	${Qt6Gui_PRIVATE_INCLUDE_DIRS}
	"${CMAKE_BINARY_DIR}/common/include"
	"${CMAKE_SOURCE_DIR}/pcsx2"
	"${CMAKE_SOURCE_DIR}/pcsx2-qt"
)

target_link_libraries(pcsx2-qt PRIVATE
	PCSX2_FLAGS
	PCSX2
	Qt6::Core
	Qt6::Gui
	Qt6::Widgets
	Qt6::Network
)

# Currently, 7z is only needed for the Windows updater.
if(WIN32)
	target_link_libraries(pcsx2-qt PRIVATE
		LZMA::LZMA
	)
endif()

setup_main_executable(pcsx2-qt)
